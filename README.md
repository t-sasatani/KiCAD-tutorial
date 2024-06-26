# KiCad tutorial

## Content (what we will make)
- Make a simple wireless power receiver circuit that lights up an LED light bulb.
- (I might add some other circuit examples by the workshop.)

## What you will learn
- The minimum workflow for using KiCad
- How to place orders to PCB manufactures
- Some elementary tips for prototyping circuits
- Final design files ([schematic](/KiCad/export/sch.pdf), [board](/KiCad/export/brd.pdf))

## What you won't learn
- Circuit design (parts selection, patterning, etc.)

# To do before workshop

## Download KiCad
- [KiCAD](https://www.kicad.org/): I'm using version 8.0.2.

## Watch short tutorial video (optional)
About 13 min
[![](https://img.youtube.com/vi/3FGNw28xBr0/0.jpg)](https://www.youtube.com/watch?v=3FGNw28xBr0)

# Hands-on workshop

## Typical workflow
DRC: Design rule check
```mermaid
flowchart TD
    B[Import/create parts] --> C[Make schematic]
    C --> B
    C --> G[Define DRC]
    G --> D[Pattern board]
    D --> C
    D --> E{DRC}
    E --> |NG| D
    E --> |OK| F{Fab review}
    F --> |NG| D
    F --> |OK| H[Order]
```

## Sketch circuit
- Roughly determine the core components you will use
    - Be careful of the availability of parts, etc
- For my case, I hand write a sketch
- We'll skip this in this tutorial

## Import/create parts
- We will use components pre-loaded in KiCad, so we'll skip this part
- If you want to make parts, watch the following video.
    - TBD

## Make schematic
### Place the components
[Schematic PDF](/KiCad/export/sch.pdf)
![](./img/schematic_done.png)
- **LDO: Voltage regulator (U1)**
    - Symbol: NCP1117-ADJ_SOT223
    - Footprint: Package_TO_SOT_SMD:SOT-223-3_TabPin2
    - [Digikey](https://www.digikey.jp/product-detail/ja/on-semiconductor/NCP1117STAT3G/NCP1117STAT3GOSCT-ND/1967218)

- **Ground: GND**
    - Symbol: GND

- **Tantalum Capacitors (C1, C2)**
    - Symbol: C_Polarized
    - Footprint: Capacitor_Tantalum_SMD:CP_EIA-3216-10_Kemet-I_Pad1.58x1.35mm_HandSolder
        - C1 = 10 uF, 25V, tant
        - C2 = 10 uF, 10V, tant
    - [Digikey-1](https://www.digikey.jp/ja/products/detail/kemet/T491A106M020AT/1739472)
    - [Digikey-2](https://www.digikey.jp/ja/products/detail/kemet/T491A106K010AT/818545)

- **Feedback resistor (R1, R2)**
    - Symbol: R
    - Footprint: Resistor_SMD:R_0603_1608Metric_Pad0.98x0.95mm_HandSolder
    - **Quiz: tune the output voltage to 9V, looking at the [LDO datasheet](https://www.onsemi.com/pdf/datasheet/ncp1117-d.pdf)**
        - R1 = ?
        - R2 = ?

- **Diode (D1, D2, D3, D4)**
    - Symbol: PMEG6010CEH
    - Footprint: Diode_SMD:D_SOD-123F
    - [Digikey](https://www.digikey.jp/product-detail/ja/nexperia-usa-inc/PMEG6010CEH-115/1727-3848-1-ND/1589917)

- **SMA connector (J1)**
    - Symbol: Conn_Coaxial
    - Footprint: Connector_Coaxial:SMA_Amphenol_901-143_Horizontal
    - [Digikey](https://www.digikey.jp/products/ja?keywords=60311002114501)

- **Ceramic capacitors: (C3, C4, C5, C6)**
    - Symbol: C
    - Footprint: Capacitor_SMD:C_0603_1608Metric_Pad1.08x0.95mm_HandSolder
    - Values
        - C3 = 1000 pF
        - C4 = 0.1 uF
        - C5 = DNP
        - C6 = 0.1 uF

- **Test point: (TP1-TP8)**
    - Symbol: TestPoint
    - Footprint: TestPoint:TestPoint_Keystone_5000-5004_Miniature
    - Vout is also this pin.

- **Mounting hole (H1-H4)**
    - Symbol: MountingHole
    - MountingHole:MountingHole_3.2mm_M3

### Tips
- Name the wires
    - This makes complex designs easier, so lets make it your habit.

## Pattern board

### Constraints
Below are just examples. You'll need to check factory design rules (for PCBWay, you can check the [PCB Instant Quote](https://www.pcbway.com/orderonline.aspx) page).
- PCBWay: https://www.pcbway.com/capabilities.html

![](./img/board_setup.png)
![](./img/constraints.png)

### Board layout
[Board layout PDF](/KiCad/export/brd.pdf)
![](./img/board_before_layout.png)
![](./img/parts_place.png)
![](./img/board_layout.png)

### Check in 3-D CAD
- Look for mechanical intersections, etc.
![](./img/3d_view.png)

## Send to fab
- [PCBWay](https://www.pcbway.com/) and [Login information](https://sites.google.com/a/akg.t.u-tokyo.ac.jp/wiki) of lab account
- Use [PCBWay plug-in for KiCad](https://github.com/pcbway/PCBWay-Plug-in-for-Kicad)
- Try out gerber viewer (beta)
    - https://www.pcbway.com/project/OnlineGerberViewer.html

# Misc

## Links
- https://componentsearchengine.com/