# System.ExecutionEngineException

## Problem

I now got several weeks a `System.ExecutionEngineException` when starting our Xamarin app build with Xamarin.Forms under UWP.

After updating to Windows 10 Build 1903 I nearly could not start the app at any time.

So I tried to track down the real cause of this problem.

The error was raised here in the UWP startup, and was not catchable or having anything detailed information beside its stupid "System.ExecutionEngineException".

```cs
public MainPage()
{
    InitializeComponent();

    var initializer = new UwpInitializer();
    var application = new App1.App(initializer);

    LoadApplication(application); //System.ExecutionEngineException
}
```

After the preinvastigation of a colleague I disabled *Enable Just My Code* in **Debugging**
and than saw at

`obj\x86\Debug\XamlTypeInfo.g.cs`

```cs
public global::Windows.UI.Xaml.Markup.IXamlType GetXamlTypeByName(string typeName)
{
    return Provider.GetXamlType(typeName); //typeName = "Windows.UI.Xaml.Controls.RevealBackgroundBrush"
}
```

an error loading some XamlTypes, an he built a workaround by loading several types before that with

```cs
var provider = new global::Microsoft.UI.Xaml.Markup.ReflectionXamlMetadataProvider();
provider.GetXamlType("Xamarin.Forms.Platform.UWP.FormsCommandBar");
//provider.GetXamlType("...
//etc.
```

This seemed to work for a while, but after my Windows Update I could not work anymore.

Some developers also reported a

- SystemViolationException

or

- Unhandled Exception: System.AccessViolationException: Attempted to read or write protected memory. This is often an indication that other memory is corrupt

## Solution

But when I finally tracked down the problem was not anything we excpected. It was nearly the last codeline I deleted from our code to track down the error AND:
It was NLog!
I am still investigating the root cause of this problem, but at the moment I removed NLog an its corresponding static LayoutRenderer method, the problem was gone.

We had two lines accessing NLog, and I needed to remove both to get a succesfully starting app again.

```cs
var loggerFactory = new LoggerFactory();
// register username as layout renderer
LayoutRenderer.Register("username", _ => "not logged in");
loggerFactory.AddNLog(Device.RuntimePlatform == Device.Android ? "assets/NLog.config" : "NLog.config");
//...
```

So I wanted to promote a solution so someone may find it useful, when searching for the problem.
