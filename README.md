
# CoreXY Whiteboard Plotter

### Turning an ordinary whiteboard into a computer-controlled drawing machine.

**A low-cost, custom-built CoreXY plotter integrated directly into a whiteboard, capable of drawing digital images and responding to hand gestures.**

> **🚧 Documentation in Progress**
>
> The physical machine is fully functional, with ongoing software development and new features planned. This repository is currently being organised, and the source code, CAD files and additional technical documentation will be added soon.

![CoreXY Whiteboard Plotter](images/TLOUELLIE.jpg)

![CoreXY Whiteboard Plotter](images/photorealistic.jpg)
---

## Overview

The idea for this project came to me shortly after starting university, where I encountered CNC machines and 3D printers properly for the first time. I became fascinated by how these machines could translate computer instructions into precise physical movements, and eventually decided I wanted to build something similar myself.

Having seen various pen plotters online, I thought it would be interesting to build one into a whiteboard. Not something that simply sits on top of a whiteboard, but a machine that feels like part of the whiteboard itself.

I also wanted to keep the cost as low as possible and avoid adding unnecessary bulk. The result is a compact, CoreXY-inspired drawing system that can reproduce digital images directly onto a **53 × 43 cm drawing area**.

Unlike some of my other projects, this one is still actively evolving. The original machine has been built and works, but its software makes it easy to keep adding new features, from hand-gesture drawing to more ambitious ideas involving AI and automated whiteboard interaction.

## Mechanical Design

The mechanism takes inspiration from CoreXY 3D printers, using two NEMA 17 stepper motors, a belt and pulley system, and a moving pen carriage. The custom mechanical components were designed in CAD and 3D printed.

One of the most useful design decisions came from an unexpected discovery. The whiteboard originally had sliding hooks intended for hanging it on a wall. I noticed that these hooks could move relatively freely along the board, so rather than purchasing another linear rail, I designed custom printed mounts that repurposed them as part of the motion system.

This saved money, reduced the number of additional components and helped keep the entire machine integrated into the existing whiteboard.

The other axis uses a purchased linear rail, while the motors, pulleys and supporting structures are mounted around the edges of the board.

The pen-lifting mechanism uses an MG995 servo and a spring-loaded carriage. Rather than relying on the servo to continuously press the marker against the board, the spring provides the drawing pressure while the servo lifts or releases the pen. This helps maintain consistent contact and reduces skipping during drawings.

The project involved plenty of design iterations, particularly while trying to keep the mechanism compact, inexpensive and reliable.

## Electronics and Control

The electronics are built around an Arduino with a CNC shield running GRBL firmware.

Two NEMA 17 stepper motors control the CoreXY movement, while an MG995 servo operates the pen-lifting mechanism. Stepper drivers were selected with noise reduction in mind, eventually moving to TMC drivers after earlier configurations produced enough vibration to annoy my flatmate.

The machine runs from a 24V power supply, with a DC-DC buck converter providing a separate low-voltage supply for the servo and cooling fan.

For cooling, I repurposed an old AMD CPU fan and mounted it above the electronics to keep the stepper drivers cool during longer drawings.

The original electronics were assembled on a breadboard, and I initially experimented with writing my own motion-control firmware. Eventually, I moved to GRBL and a CNC shield, which provided a more compact and reliable solution while allowing me to retain the custom software functionality I wanted.

## Software and Features

The plotter is controlled through a custom Python application that communicates with the Arduino over USB serial.

The software allows me to import images, process them into drawing paths, and convert those paths into G-code. These drawings can then be positioned and resized within a graphical representation of the whiteboard before being sent to the machine.

The image-processing pipeline includes skeletonisation and vectorisation, allowing black-and-white line drawings to be reproduced using an ordinary whiteboard marker. The machine can also attempt more detailed images, although simpler line drawings generally produce the best results.

Another feature I've experimented with is something I call **Air Drawing**.

Using a webcam and MediaPipe hand tracking, the software follows my hand movements in two-dimensional space and translates them into movements of the pen carriage. Hand gestures control whether the pen is raised or lowered, allowing me to draw in the air while the machine reproduces the movements on the whiteboard.

This has been one of the more entertaining additions to the project, and demonstrates how easily the machine can be extended beyond conventional image plotting.

## Future Development

One of my favourite things about this project is that there's always something else I can add to it.

My next major goal is to integrate an erasing mechanism, allowing the plotter not only to draw on the whiteboard but also to remove existing content.

From there, I'd like to experiment with connecting the system to a local AI assistant. One idea is to turn the whiteboard into a physical, automatically maintained to-do list, where tasks can be written, erased and updated through voice commands.

I'd also like to explore AI-generated drawings. For example, I could ask the system to draw a cat, have an image-generation model produce a suitable line drawing, and then process that image into G-code for the plotter to draw automatically.

For now, the machine is fully functional as a computer-controlled whiteboard plotter, with plenty of room for new features and improvements.

---

*This is an ongoing independent engineering project. Source code, CAD models and further documentation will be added to this repository as development continues.*
