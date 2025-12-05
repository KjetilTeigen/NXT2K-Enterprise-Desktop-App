# NXT-2000 Enterprise Desktop Application

**Version: 1.0.0**

This document serves as the primary reference guide for the NXT-2000 Enterprise spectrum analyzer application.

## 1. Application Architecture

The NXT-2000 application is designed as a standalone desktop executable (EXE/DMG). It uses the following components to manage device communication and visualization:

| Component | Role | Functionality |
| :--- | :--- | :--- |
| **Main Interface** | Visualization and controls | The primary window handling all user input, charting, and visual display. |
| **Backend Engine** | Serial Communication | Manages the USB hardware connection and controls the proprietary command protocols. |
| **3D Visualization** | External Library | Utilizes the powerful **Three.js** library to render interactive 3D spectral waterfalls. |

## 2. Spectrum Visualization and Display Features

The main canvas is divided into the Spectrum View (top) and the Waterfall/3D View (bottom).

### A. Real-Time Traces

These traces show amplitude (Y-axis, $\text{dBm}$) vs. frequency (X-axis).

| Trace | Color (Default) | Purpose |
| :--- | :--- | :--- |
| **Realtime** | Green | Shows the current, smoothed amplitude of the radio environment. This is the **live** view. |
| **Max Hold** | Red | Captures and displays the highest signal recorded at each frequency since the last reset. Essential for detecting intermittent signals. |
| **Average** | Blue/Cyan | Displays the weighted moving average of the signal over time. This creates a stable baseline for background power/noise level. |

### B. Spectral Density / Persistence

This feature helps visualize how often energy appears at a specific frequency over time.

* **Function:** Toggled by the **Enable Heatmap** checkbox.

* **Mechanism:** The view utilizes a **Phosphor Persistence** effect, where previous spectrum sweeps are drawn with gradually decreasing opacity.

* **Result:** High-activity signals leave a visible "trail" (density) on the screen, mimicking the persistence of a traditional CRT spectrum analyzer.

* **Control:** The **Persistence slider** controls the decay rate, defining how long the trails remain visible.

### C. Channel Utilization and Status

The application provides immediate visual feedback on key operational metrics:

| Feature | Location | Benefit |
| :--- | :--- | :--- |
| **Utilization %** | Directly below Channel ID (Top of Spectrum) | Shows the percentage of time the channel energy exceeds a preset power threshold ($\text{Tx}/\text{Rx}$). Provides instant insight into network traffic congestion. |
| **SATURATION** | Header (Red Pill) | Appears as a solid red warning for **3 seconds** when the device reports an input overload. Indicates that the signal input is too strong and measurements may be inaccurate. |
| **3D Spectrum View** | Bottom View (Toggled by Button) | Displays the spectral history as a three-dimensional waterfall. The history data is continuously recorded in the background, ensuring the full graph is visible instantly when switching between bands or views. |

## 3. Operational Controls

### A. Recording Studio

The Recording Studio enables saving and playback of spectrum data for analysis or documentation.

| Control | Function | File Format |
| :--- | :--- | :--- |
| **REC/STOP REC** | Captures raw spectrum data sweeps into a volatile buffer. | N/A |
| **PLAY/PAUSE** | Plays back captured data frames into the visualization. | N/A |
| **SAVE** | Exports the captured data buffer. | `.nxt` (Custom ASCII Hex Encoded) |
| **LOAD** | Imports previously saved data. | `.nxt` (Custom ASCII Hex Encoded) |

### B. Calibration and Device Control

| Control | Function | Role |
| :--- | :--- | :--- |
| **Sensitivity (1.4)** | **Primary Calibration Factor.** | Multiplies the raw input amplitude to align the visual $\text{dBm}$ value with standardized external measurements. The $1.4$ value is the required calibration factor for this hardware. |
| **dB Offset** | Fine tuning adjustment (user selectable). | Shifts the entire vertical display up or down without affecting the core calibration factor. |
| **APPLY BAND** | Triggers the device to switch its scanning range (e.g., $2.4 \text{ GHz}$ to $5 \text{ GHz}$). | Ensures that the spectrum canvas immediately adjusts its horizontal scale to match the new frequency boundaries. |
