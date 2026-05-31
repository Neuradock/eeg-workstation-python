# NeuraDock EEG Development Tutorials

This repository provides Python tutorials for the NeuraDock dry-electrode EEG device, covering the full pipeline from raw data reading, real-time streaming, offline quality inspection, to signal analysis.

---

## Tutorial Index (7 Lessons)

| No. | File | Description |
| :-- | :--- | :---------- |
| 1 | `1.text_file_read_bluetooth_version.ipynb` | **Bluetooth Offline Data Reading**: Parse the `.txt` log file saved by NeuraDock (Bluetooth mode) into a NumPy array `[channels, data_points]`, and visualize basic time-domain waveforms. |
| 2 | `2.text_file_read_usb_version.ipynb` | **USB Offline Data Reading**: Similar to Tutorial 1, but adapted to the USB data format (1 sample packet per line instead of 5). |
| 3 | `3.online_data_stream_bluetooth.ipynb` | **Bluetooth Online Data Stream**: Receive EEG data in real time via TCP, fetching and processing data segment by segment. |
| 4 | `4.online_data_stream_usb.ipynb` | **USB Online Data Stream**: Receive EEG data in real time via TCP, suitable for high-sampling-rate scenarios. |
| 5 | `5.offline_data_quality_check.ipynb` | **Offline Signal Quality Check**: Perform segment-wise Welch PSD analysis on existing data, evaluate signal quality from three perspectives—50Hz power-line noise, EMG artifacts, and outliers—and generate heatmaps. |
| 6 | `6.offline_data_preprocess.ipynb` | **Offline Data Preprocessing**: Based on the quality-check results from Tutorial 5, automatically detect bad channels, reject noisy time segments, and provide before/after comparison visualizations. |
| 7 | `7.signal_quality_check.ipynb` | **Comprehensive Signal Quality Assessment**: Demonstrate two classic EEG paradigms—eyes-open/closed Alpha Blocking and task-state ERD (Event-Related Desynchronization)—and plot topographic maps (Topomaps) using MNE. |

---

## Core Dependencies

```
numpy, pandas, matplotlib, scipy, seaborn, mne
```

For the full dependency list, please see [`requirements.txt`](requirements.txt).

---

## Environment Requirements

- **Python Version**: **3.9 or 3.10** is recommended for the best compatibility.  
  See [`PYTHON_VERSION.md`](PYTHON_VERSION.md) for details.
- **Operating System**: Windows / macOS / Linux (online streaming tutorials require the device and PC to be on the same LAN).

---

## Quick Start

1. **Clone the repository**
   ```bash
   git clone <repo-url>
   cd NeuraDock-Tutorials
   ```

2. **Create a virtual environment**
   ```bash
   python3.10 -m venv venv
   # Windows
   venv\Scripts\activate
   # macOS / Linux
   source venv/bin/activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Run the tutorials**
   ```bash
   jupyter notebook
   ```
   Open the notebooks in order: `1` → `2` → `3` / `4` → `5` → `6` → `9`.

---

## Supplementary Files

- **`Neuradock_library.py`**: Core algorithm library that encapsulates Bluetooth/USB data parsing, quality checks, data cleaning, and Alpha analysis. Tutorials 5, 6, and 9 depend on this module.
- **`7.neuradock_marker.py`**: Online experiment marker tool. Provides `DataStream` and `EEGThreadManager` classes for injecting event markers during real-time acquisition.
- **`example_data_bluetooth.txt` / `example_data_usb.txt`**: Example data files for direct use in offline tutorials.

---

## Learning Path

1. **Offline Basics**: Start with Tutorial 1 or 2 to get familiar with the `.txt` file format and parsing logic.  
2. **Online Streaming**: After understanding the offline data format, use Tutorial 3 or 4 to connect the device and experience real-time streaming.  
3. **Quality Control**: Run Tutorials 5 and 6 to build an intuitive understanding of EEG noise (powerline, EMG, outliers) and learn the cleaning strategy.  
4. **Comprehensive Assessment**: Tutorial 9 is application-oriented. Validate signal quality and device performance through classic paradigms and topographic mapping.

---

## Notes

- Tutorials 3 and 4 require the NeuraDock device to enable TCP data forwarding, and the PC must be on the same LAN as the device.
- The topographic analysis in Tutorial 9 relies on standard 10-20 electrode positions. The current 7-channel data is approximately projected using the `GSN-HydroCel-128` montage.
- All threshold parameters (e.g., `thresh = [10, 20, 2]`) are set based on NeuraDock hardware characteristics. Please adjust them according to your actual application scenario.
