# ArduinoBP

ArduinoBP is a visual tool that lets you build Arduino code using a node-based system, kind of like Unreal Engine's Blueprints. Instead of writing code manually, you drag and connect nodes, and the C++ code is generated for you—ready to copy and paste into the Arduino IDE.

## What is this?

ArduinoBP was built to make Arduino development easier and more fun, especially for people who like to think visually. It supports everything from basic math and logic to sensors, MP3 playback, TFT displays, and more. You can even build your own custom libraries and extend the system however you want.

This project runs on top of LiteGraph.js and adds a ton of features.

## How does it work?

1. You start by placing a `Setup` and `Loop` node.
2. Then you drag in other nodes like `Print`, `If`, `Add`, or sensor readers.
3. Connect them to define the logic visually.
4. Click "Generate Code" and it will spit out clean, ready-to-run C++ code.

## Example Projects

I'll be adding photos and videos soon to show some examples. If you want to contribute your own, feel free to share them with me!

## Node Highlights

Here are some node types you’ll find:

- **Flow Control:** Branch, DoOnce, ForLoop, While, Gate, FlipFlop, MultiGate
- **Math:** Add, Subtract, Multiply, Divide, Modulo (for Int, Float, Byte, and more)
- **Logic:** Equal, Not Equal, Greater, Less, etc.
- **Variables:** Int, Float, Bool, Byte, String, Color, Vector3 – including arrays (WIP)
- **Debugging:** Print, PrintCleanString (replaces line in Serial Monitor)
- **Sensors:** VL53L0X, MPU6050, MPU9250, MPU9262, and more (Any request to sensors you can ask on Discord, and follow actual request on Trello)

## Community

If you're working on a project, stuck on something, or just want to talk ideas, come hang out on Discord. We’re building a small but helpful community.

Discord: [https://discord.gg/mxsfKku7JV]

## Support ArduinoBP

ArduinoBP is a labor of love, built with passion and countless hours of dedication.  
If this project has helped you in any way, consider supporting it — every bit of help keeps it alive and fuels the motivation to keep building and sharing.  
**Thank you for being part of this journey.**

[![Donate](https://img.shields.io/badge/Donate-PayPal-blue.svg)](https://www.paypal.com/donate/?hosted_button_id=RHHMMWMGAYZH8)



Anything helps and keeps the project going!

## Project Layout

This repo includes:

- ArduinoBP executable Files
- Libraries for things like MP3 playback, TFT drawing, sensors
- Example `.abp` graph files

## Requirements

- Arduino IDE
- A supported board (like Arduino Uno, ESP32-S3, etc.)
- If you want to customize, some knowledge of C++ or JS will help

---

This is still a work-in-progress and growing every day. If you want to contribute, test, or just chat, I’d love to hear from you!

## 📚 Documentation

Here you will find a collection of tutorials, usage examples, and guides to help you get the most out of **ArduinoBP**.

---

### 🔧 Getting Started

**Description:**  
You will still need the Arduino IDE to compile the code. ArduinoBP includes a tool to export `.ino` files.  
Make sure you have installed the necessary libraries corresponding to the `#include` statements in your code, just like you normally would when coding manually.


---

### 🧠 Node System Overview

**Description:**  
Understand how the visual node system works, how nodes are connected, and how flow and data types interact to generate valid Arduino code.

**Image:**  
![Node System Overview](docs/images/node-system.png)

**Video:**  
[![Watch on YouTube](https://img.youtube.com/vi/YOUTUBE_ID_2/0.jpg)](https://www.youtube.com/watch?v=YOUTUBE_ID_2)

---

### ⚙️ Custom Nodes & Libraries

**Description:**  
Learn how to create your own custom nodes, import libraries, and expand ArduinoBP for any hardware.

**Image:**  
![Custom Nodes](docs/images/custom-nodes.png)

**Video:**  
[![Watch on YouTube](https://img.youtube.com/vi/YOUTUBE_ID_3/0.jpg)](https://www.youtube.com/watch?v=YOUTUBE_ID_3)

---

### 🔁 Flow Control Examples

**Description:**  
See examples of how to use Branch, Delay, ForLoop, DoOnce and other powerful flow-control nodes.

**Image:**  
![Flow Control Example](docs/images/flow-control.png)

**Video:**  
[![Watch on YouTube](https://img.youtube.com/vi/YOUTUBE_ID_4/0.jpg)](https://www.youtube.com/watch?v=YOUTUBE_ID_4)

---

### 📤 Exporting & Uploading Code

**Description:**  
Step-by-step guide to exporting generated code and uploading it to your Arduino via the Arduino IDE.

**Image:**  
![Export Code](docs/images/export-code.png)

**Video:**  
[![Watch on YouTube](https://img.youtube.com/vi/YOUTUBE_ID_5/0.jpg)](https://www.youtube.com/watch?v=YOUTUBE_ID_5)

