# PrusaSlicer settings for the Geeetech Prusa i3 Pro

A while ago I wanted to get started with 3D printing, so my wife bought me a simple DIY 3D printing kit from the chinese company Geeetech. So after assembling the whole thing together with my son, and the first try and errors with the Easy Print 3D software from Geeetech and weeks of printing with Cura 3D, I wanted to get PrusaSlicer to work because of some features I like there a lot, for example to print a brim and a skirt and so on. So after researching the Internet for a while, a reading the builtin settings from the printer from the display and via G-Codes I disovered the following settings are working fine for my Geeetech Prusa i3 Pro W but I think for every other Geeetech Prusa i3 variant too. So I wanted to share them, and here they are (mostly only the settings different from the default values of PrusaSlicer 2.2.0)

## Printer Settings

`Geeetech Prusa I3 Pro W`

### General

`180`,`225`,`200`

### Firmware

- `Marlin`
- Supports stealth mode: `false`

### Custom G-code

#### Start G-code

```gcode
G28 ;Home
G1 Z15.0 F6000 ;Move the platform down 15mm
G92 E0
G1 F200 E3
G92 E0
```

#### End G-code

```gcode
M104 S0;Cooling the heat end
M140 S0;Cooling the heat bed
G92 E1
G1 E-1 F300
G28 X0 Y0;Home X axis and Y axis
M84
```

### Machine limits

#### Maximum feedrates

- Maximum feedrate Y: `400` mm/s
- Maximum feedrate Y: `400` mm/s
- Maximum feedrate Z: `2` mm/s
- Maximum feedrate E: `45` mm/s

#### Maximum accelerations

- Maximum acceleration X: `5000` mm/s2
- Maximum acceleration Y: `5000` mm/s2
- Maximum acceleration Z: `50` mm/s2
- Maximum acceleration E: `5000` mm/s2
- Maximum acceleration when extruding: `1000` mm/s2
- Maximum acceleration when retracting: `2000` mm/s2

#### Jerk limits

- Maximum jerk X: `20` mm/s
- Maximum jerk Y: `20` mm/s
- Maximum jerk Z: `0.4` mm/s
- Maximum jerk X: `5` mm/s

#### Minimum feedrates

- Minimum feedrate when extruding: `0`mm/s
- Minimum travel feedrate: `0`mm/s

### Extruder 1

#### Size

- Nozzle diameter: `0.4` mm

#### Layer height limits
- Min: `0.1` mm
- Max: `0.3` mm

#### Retraction

- Length: `0.5` mm
- Retraction Speed: `8` mm/s
- Minimum travel after retraction: `5` mm

## Print Settings

### Layers and perimeters

Layer height: `0.2`,`0.3`

### Horizontal shells

`5`,`3`
`0`,`0`

### Infill

- Fill pattern: `Rectlinear`

### Speed

#### Speed for print moves

`30`,`10`,`50%`,`30`,`15`,`10`,`30`,`100%`,`60`,`10`

#### Speed for non-print moves

`80`

#### Modifiers

`10`

#### Auto Speed

`20`,`0`

## Print Settings (speed)

#### Speed for print moves

`45`,`15`,`50%`,`60`,`20`,`15`,`30`,`100%`,`60`,`20`

#### Speed for non-print moves

`90`

#### Modifiers

`15`
