# ArduinoBP

ArduinoBP is a visual tool that lets you build Arduino code using a node-based system, kind of like Unreal Engine's Blueprints. Instead of writing code manually, you drag and connect nodes, and the C++ code is generated for you—ready to copy and paste into the Arduino IDE.

## What is this?

ArduinoBP was built to make Arduino development easier and more fun, especially for people who like to think visually. It supports everything from basic math and logic to sensors, MP3 playback, TFT displays, and more. You can even build your own custom libraries and extend the system however you want.

This project runs on top of LiteGraph.js and adds a ton of features.

**Image:**  
![Getting Started Screenshot](docs/Image_01.png)

## How does it work?

1. You start by placing a `Setup` and `Loop` node.
2. Then you drag in other nodes like `Print`, `If`, `Add`, or sensor readers.
3. Connect them to define the logic visually.
4. Click "Generate Code" and it will spit out clean, ready-to-run C++ code.


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

# 📚 Documentation

Here you will find a collection of tutorials, usage examples, and guides to help you get the most out of **ArduinoBP**.

---

## 🔧 Getting Started

**Description:**  
You will still need the Arduino IDE to compile the code. ArduinoBP includes a tool to export `.ino` files.  
Make sure you have installed the necessary libraries corresponding to the `#include` statements in your code, just like you normally would when coding manually.


---

## 🧠 Node System Overview

**Description:**  
Understand how the visual node system works, how nodes are connected, and how flow and data types interact to generate valid Arduino code.

---

ArduinoBP is inspired by the **Blueprint system from Unreal Engine**, where logic is built visually using connected nodes.

The system has been **adapted specifically for Arduino development**, meaning it follows the microcontroller execution model using two entry points:

- **`Setup` node:** Corresponds to Arduino's `setup()` function. Runs once at startup.
- **`Loop` node:** Corresponds to Arduino's `loop()` function. Runs continuously.

---

### 🔁 Flow System

The core execution logic uses **Flow pins and Flow links**, which control the order in which nodes are executed.

- **Flow Input**: Where execution enters the node.
- **Flow Output**: Where execution continues to the next node.

When you connect one node's Flow Output to another's Flow Input, you are **defining execution order**, similar to sequential lines of code.

Example:
```
[Setup] → [AHTBegin] → [AHTUpdate] → [PrintTemperature]
```
This sequence ensures each node is called in order during the program's `setup()`.

---

### 🔗 Data Pins

In addition to Flow pins, nodes can have **typed input and output pins** like `Int`, `Float`, `Bool`, or `String`.

- Data pins **transfer values**, not execution.
- You can connect outputs from one node to the inputs of another to pass values along the flow.

This allows combining logic like:
```
[Sensor Read] → [Float] → [Compare] → [Branch]
```

Together, the **Flow + Data** system allows ArduinoBP to visually express complete Arduino logic in a user-friendly and intuitive way.

---



## ⚙️ Setting Examples and Library

**Description:**  
Before you can use custom nodes or explore the examples, you need to tell ArduinoBP where to find your libraries and example files.

---

### 🔧 How to Set Paths

1. Open ArduinoBP.
2. From the **top menu**, click on **"Tool" > "Settings"**.
3. In the settings window, locate:
   - **Library Path** – this is where your custom libraries (`.h` files) are stored.
   - **Examples Path** – this is the folder containing your `.abp` project files.

Set each field to the correct folder on your system (e.g., `D:/ArduinoLibrary/` for libraries and `D:/ArduinoBPExamples/` for examples).  
Once set, these resources will be automatically loaded every time you open the editor.

---

### 🖼️ Interface

Below is a screenshot of the settings screen:

![Settings Screen](docs/Image_02.png)

---

## ⚙️ Custom Nodes & Libraries

**Description:**  
Learn how to create your own custom nodes, import libraries, and expand ArduinoBP for any hardware.

ArduinoBP allows you to expand functionality by creating custom libraries that define new variable types and nodes.  
These libraries are automatically parsed at startup and become available in the editor.

### 🧩 How Custom Libraries Work

A custom library is a `.h` file placed in your `D:/ArduinoLibrary/` folder. ArduinoBP scans this folder and parses each file using a specific structure. Below is a breakdown using a real example for the **Adafruit AHTX0** sensor.

---

#### 🔸 Library Variables Block
```cpp
VAR: aht, Object, , DECL: Adafruit_AHTX0 aht;
VAR: aht_temp, Float, 0.0f;
VAR: aht_humidity, Float, 0.0f;
```

Each `VAR:` line defines a global variable used by the library:

- **Syntax:**  
  `VAR: name, type, default_value, [optional DECL override]`

- **Parameters:**  
  - `name`: internal name used in the code (must be unique).
  - `type`: variable type (e.g., `Float`, `Bool`, `Object`).
  - `default_value`: initial value. Leave blank if not needed.
  - `DECL:`: optional custom declaration, useful for objects.

- **Example:**
  ```cpp
  VAR: aht, Object, , DECL: Adafruit_AHTX0 aht;
  ```
  This declares:
  ```cpp
  Adafruit_AHTX0 aht;
  ```

  Another:
  ```cpp
  VAR: aht_temp, Float, 0.0f;
  ```
  This declares:
  ```cpp
  float aht_temp = 0.0f;
  ```

---

### 🧩 Defining Nodes

Each node is defined using the `NODE:` syntax:

```cpp
NODE: AHTBegin {
    Name = AHT Begin;
    InternalName = AHTBegin;
    Color = (100, 200, 255);
    Include = Adafruit_AHTX0.h;
    Description = "Initializes the AHT sensor";

    Input: Flow In;
    Output: Flow Out;
}
```

#### 🔹 Node Fields:

- `Name`: Display name in the editor.
- `InternalName`: Internal unique name.
- `Color`: RGB node color in the graph.
- `Include`: Header file(s) required.
- `Description`: Tooltip shown on hover.
- `Input` / `Output`: Define pins. Can be `Flow`, or typed pins like `Float`, `Bool`, etc.

---

### 🔧 CODE Block

Each node can include a code block that defines the actual C++ code ArduinoBP will inject during generation.

```cpp
CODE: AHTBegin
    aht.begin();
END_CODE
```

- The code **starts on the line immediately after** `CODE: <FunctionName>`  
- It **ends on the line right before** `END_CODE`
- Everything between those lines will be inserted as-is in the generated `.ino` file.

If the node is part of the **execution flow**, the code will be placed in the correct flow position (inside `setup()`, `loop()`, or another node chain).  
If the node is **output-only**, like `AHTGetTemperature`, the code must return a value expression:

```cpp
CODE: AHTGetTemperature
    aht_temp
END_CODE
```

This expression will be used wherever the node output is connected — for example, in another node's assignment or condition.

---


---

### 📌 Summary of AHT Nodes

| Node              | Purpose                                |
|-------------------|----------------------------------------|
| `AHTBegin`        | Initializes the sensor                 |
| `AHTUpdate`       | Updates temp and humidity values       |
| `AHTGetTemperature` | Returns the latest temperature       |
| `AHTGetHumidity`  | Returns the latest humidity            |

---

### 🧠 Custom Tips

- You can define as many variables as needed using `VAR:` and they are globally accessible.
- Use `DECL:` to create object instances or custom types.
- All nodes using the same variable set should be grouped in one file.
- You can add multiple `Include =` lines if needed; each will become a `#include` in the final `.ino`.

---

📁 Make sure your `.h` file is placed in the `D:/ArduinoLibrary/YourLibrary/` folder and named accordingly.  
Once loaded, the nodes and variables will be available automatically in the editor.


---



## 📤 Exporting & Uploading Code

**Description:**  
Once your node graph is ready, you can export it to a valid `.ino` file and upload it using the Arduino IDE.

---

### 📁 How to Export

1. Go to the **top menu** and select **"Export As..."** or press `Ctrl + I`.
2. Choose either:
   - A `.ino` file (inside a folder with the same name)
   - A folder to create a new `.ino` inside automatically

> 📌 If the `.ino` file or folder does not exist, ArduinoBP will create a folder with the same name as the `.ino`, as required by the Arduino IDE for proper compatibility.

---

### 🚀 Uploading the Code

After exporting:

1. Open the exported `.ino` file in the **Arduino IDE**
2. Make sure all required libraries (`#include`) are installed
3. Select the correct board and COM port
4. Click **Upload** to flash the code onto your Arduino

ArduinoBP generates code that is fully compatible with the Arduino IDE, so you can follow the usual steps for uploading based on your board (e.g., Uno, Mega, ESP32, etc.).


## Example Projects

I'll be adding photos and videos soon to show some examples. If you want to contribute your own, feel free to share them with me!
