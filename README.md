# NeuraDock EEG Tutorials

Python tutorials for the **NeuraDock** dry-electrode EEG device, covering offline data reading, real-time streaming, signal preprocessing, and classic EEG paradigm analysis.

---

## Repository Structure

```
examples
├── 1.text_file_read_bluetooth_version.ipynb   # Bluetooth offline data reading
├── 2.text_file_read_usb_version.ipynb         # USB offline data reading
├── 3.online_data_stream_bluetooth.ipynb       # Bluetooth real-time streaming
├── 4.online_data_stream_usb.ipynb             # USB real-time streaming
├── 5.offline_data_preprocess.ipynb            # Offline signal preprocessing
├── 6.example_study.ipynb                      # Comprehensive example study (Alpha Blocking & ERD topomaps)
├── Neuradock_library.py                       # Core EEG processing library
└── requirements.txt                           # Python dependencies
```

---

## Environment Requirements

- **Python**: 3.9 – 3.11
- **Key dependencies**: `numpy`, `scipy`, `matplotlib`, `pandas`, `seaborn`, `mne`

Install dependencies:

```bash
pip install -r requirements.txt
```

---

## Tutorial Index

| # | Notebook | Description |
|---|----------|-------------|
| 1 | `1.text_file_read_bluetooth_version.ipynb` | Parse NeuraDock Bluetooth `.txt` logs into NumPy arrays and visualize raw waveforms. |
| 2 | `2.text_file_read_usb_version.ipynb` | Parse NeuraDock USB `.txt` logs (1 packet per line) into NumPy arrays. |
| 3 | `3.online_data_stream_bluetooth.ipynb` | Receive EEG data in real time via TCP (Bluetooth mode), process segment by segment. |
| 4 | `4.online_data_stream_usb.ipynb` | Receive EEG data in real time via TCP (USB mode). |
| 5 | `5.offline_data_preprocess.ipynb` | Offline preprocessing: quality check, artifact rejection, signal cleaning, and bad-channel handling. |
| 6 | `6.example_study.ipynb` | Comprehensive example study: Eyes-Open/Closed Alpha Blocking and Task/Rest ERD analysis with MNE topographic maps. |

> **Note**: The original Tutorial 6 (`offline_text2clean_data.ipynb`) has been removed; its content is now integrated into Tutorial 5.

---

## Data Format

NeuraDock exports raw EEG data as comma-delimited `.txt` files:

- **Sampling Rate**: 250 Hz
- **Channels**: 7 (mapped to O1, O2, Oz, PO3, PO4, CP5, CP6 in the 10–20 system)
- **Bluetooth format**: 5 sample packets per line (7 channel values + 1 separator per packet)
- **USB format**: 1 sample packet per line (2 header fields + 7 channel values + 1 separator)

Use `Neuradock_library.text2data_bluetooth()` or `text2data_usb()` to parse them into `(7, N)` NumPy arrays.

---

## Quick Start

```python
from Neuradock_library import text2data_bluetooth

# Parse your own Bluetooth-format .txt file
eeg_data = text2data_bluetooth("your_data.txt")
print(eeg_data.shape)  # (7, N)
```

Open any `.ipynb` file in Jupyter and run the cells sequentially. Each notebook is self-contained and includes step-by-step explanations.
