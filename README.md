# NXT-2000 Enterprise Desktop Application

This document serves as the primary reference guide for the **NXT-2000 Enterprise spectrum analyzer** application made possible using **Gemini AI**, the tool only works with the **Netally NXT-2000 Wi-Fi Spectrum Analyzer**. 

Current newest version is **Version: 1.0.7**

<img width="1382" height="940" alt="image" src="https://github.com/user-attachments/assets/5e5468e9-6fa2-4dad-8213-b98695ebb099" />

## 1. Application Architecture

The NXT-2000 application is designed as a standalone desktop executable (EXE/DMG), compiled using Electron. It uses the following components to manage device communication and visualization:

| Component | Role | Functionality |
| :--- | :--- | :--- |
| **Main Interface** | Visualization and controls | The primary window handling all user input, charting, and visual display. |
| **Backend Engine** | Serial Communication | Manages the USB hardware connection and controls the command protocols. |
| **3D Visualization** | Integrated  Library | Utilizes the powerful Three.js library and its OrbitControls component, which are bundled within the application, to render interactive 3D spectral waterfalls. |

### A. Band Selection

A dropdown menu allows selection of the following bands: 2.4 GHz, 5 GHz, and 6 GHz. The 'Band Off' option is used to disable the device, enabling playback of recorded data

## 2. Spectrum Visualization and Display Features

The main canvas is divided into two primary views: the Spectrum View (top) and the Waterfall/3D View (bottom).

* You can add live markers by double left-clicking on the screen.
* The application supports Peak Search to automatically locate the strongest signal within the displayed frequency range.
* An amplitude distribution window is located on the side, showing the amount of signals seen, which are mostly thermal-noise.

### A. Real-Time Traces

These traces show amplitude (Y-axis, $\text{dBm}$) vs. frequency (X-axis).

| Trace | Color (Default) | Customization | Purpose | 
 | ----- | ----- | ----- | ----- | 
| **Realtime** | Green | Customizable via Color Picker | Shows the current, smoothed amplitude of the radio environment. This is the **live** view. | 
| **Max Hold** | Red | Customizable via Color Picker | Captures and displays the highest signal recorded at each frequency since the last reset. Essential for detecting intermittent signals. | 
| **Average** | Blue/Cyan | Customizable via Color Picker | Displays the weighted moving average of the signal over time. This creates a stable baseline for background power/noise level. |

### B. Spectral Density / Persistence

This feature helps visualize how often energy appears at a specific frequency over time.

* **Function:** Toggled by the **Enable Heatmap** checkbox.

* **Mechanism:** The view utilizes a Phosphor Persistence effect, where previous spectrum sweeps are drawn with gradually decreasing opacity. (Note: This function performs heavy drawing and may slow down the application, particularly on older systems.)

* **Result:** High-activity signals leave a visible "trail" (density) on the screen, mimicking the persistence of a traditional CRT spectrum analyzer.

* **Control:** The **Persistence slider** controls the decay rate, defining how long the trails remain visible.

### C. Channel Utilization and Status

The application provides immediate visual feedback on key operational metrics:

| Feature | Location | Benefit |
| :--- | :--- | :--- |
| **Utilization %** | Directly below Channel ID (Top of Spectrum) | Shows the percentage of time the channel energy exceeds a preset power threshold ($\text{Tx}/\text{Rx}$). Provides instant insight into network traffic congestion. |
| **SATURATION** | Header (Red Pill) | Appears as a solid red warning for **5 seconds** when the device reports an input overload. Indicates that the signal input is too strong and measurements may be inaccurate. |

<img width="1225" height="475" alt="image" src="https://github.com/user-attachments/assets/facccac2-5e0d-48d1-ac70-587103b9a1a3" />

### D. 3D Spectrum View

The 3D Spectrum View is located in the bottom view pane and is toggled via the view button.

* **Function:** Displays the spectral history as a three-dimensional waterfall plot.

* **Background Recording:** : History data is continuously recorded in the background, ensuring the full graph is instantly visible when switching between bands or views.

## 3. Operational Controls

### A. Recording Studio

The Recording Studio enables saving and playback of spectrum data for analysis or documentation.

| Control | Function | File Format |
| :--- | :--- | :--- |
| **REC/STOP REC** | Captures raw spectrum data sweeps into a volatile buffer. | N/A |
| **PLAY/PAUSE** | Plays back captured data frames into the visualization. | N/A |
| **SAVE** | Exports the captured data buffer. | `.nxt` (Custom ASCII Hex Encoded) |
| **LOAD** | Imports previously saved data. | `.nxt` (Custom ASCII Hex Encoded) |

### D. Advanced Tuning

Fine-tune the visualization and calibration of the device.

| Setting | Description |
| :--- | :--- |
| **View Split** | Adjusts the vertical size ratio between the 2D Spectrum and 3D Waterfall views. |
| **dB Offset** | Fine tuning adjustment (user selectable). Shifts the entire vertical display up or down without affecting the core calibration factor. |
| **Smoothness** | Increases the averaging window for the Realtime trace to reduce noise jitter. |
| **Sensitivity** | Primary Calibration Factor. Multiplies the raw input amplitude to align the visual `dBm` value with standardized external measurements. Default is 1.0. Adjusting this slider allows alignment with an external reference device. |
| **Waterfall Palette** | Selects the color scheme for the waterfall (e.g., Turbo, Classic, Inferno). |

## 4. System Information

### A. System Logs

The application maintains an internal log of connection events and errors, visible in the **SYSTEM LOGS** widget at the bottom of the sidebar.

### B. Installation Location

By default, the application installs to the user's local program data folder to ensure permissions are handled correctly without requiring admin rights for updates.

* **Windows:** `%LOCALAPPDATA%\Programs\NXT-2000 Enterprise`

