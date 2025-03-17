---

# Dental Cavity Detection

This project is a dental cavity detection system using YOLOv5. It is designed to analyze dental images and detect cavities using a trained deep learning model.

## Features

- **Real-time Detection:** Detect cavities in dental images or live video streams.
- **Custom Training:** YOLOv5 is trained on a custom dataset of dental X-rays.
- **High Accuracy:** Uses a pretrained model fine-tuned for dental image analysis.

## Requirements

Ensure the following are installed:

- Python 3.8 or above
- Torch (PyTorch)
- OpenCV
- YOLOv5
- Raspberry Pi (optional for embedded use)
- Camera Module (e.g., Pi Camera 3 Noir)

### Python Dependencies

Install required Python libraries using:
```bash
pip install -r requirements.txt
```

Example `requirements.txt`:
```
torch
opencv-python
numpy
matplotlib
pandas
seaborn
PyYAML
tqdm
```

## Installation

1. **Clone the Repository:**
   ```bash
   git clone https://github.com/yourusername/dental-cavity-detection.git
   cd dental-cavity-detection
   ```

2. **Download or Train YOLOv5 Weights:**
   - Pretrained weights can be downloaded and placed in the `weights` directory.
   - Alternatively, train a YOLOv5 model on your dental dataset:
     ```bash
     python train.py --data data/dental.yaml --cfg models/yolov5s.yaml --weights yolov5s.pt --epochs 100
     ```

3. **Connect a Camera (if using live detection):**
   - Ensure your Raspberry Pi camera is enabled and recognized.

## Usage

### For Real-Time Detection:
Run the following command for live detection:
```bash
libcamera-vid --camera 0 --width 640 --height 480 --framerate 30 --output - | python3 detect.py --source pipe:0 --weights weights/last.pt --img-size 640 --conf-thres 0.5 --view-img
```

### For Image Detection:
Use this command to detect cavities in a static image:
```bash
python detect.py --source data/images/sample.jpg --weights weights/last.pt --img-size 640 --conf-thres 0.5 --view-img
```

### For Video Detection:
Run detection on a video file:
```bash
python detect.py --source data/videos/sample.mp4 --weights weights/last.pt --img-size 640 --conf-thres 0.5 --view-img
```

## Dataset

The dataset includes dental X-rays annotated for cavity detection. Ensure the dataset is in the correct YOLO format (images and `.txt` files for labels). Update the dataset path in `data/dental.yaml`:
```yaml
train: ../data/dental/train
val: ../data/dental/val
test: ../data/dental/test
```

## Results

Results will be saved in the `runs/detect` directory by default. Each detection run generates:

- Annotated images/videos with bounding boxes for cavities.
- Logs and performance metrics.

## Troubleshooting

- If the camera is not detected, ensure `libcamera` is properly configured:
  ```bash
  libcamera-hello
  ```
- For OpenCV-related issues, verify its installation:
  ```bash
  pip install opencv-python
  ```

## Future Improvements

- Add support for additional dental conditions.
- Optimize detection speed and model performance.
- Deploy the system on a cloud platform for scalability.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Acknowledgments

- YOLOv5 by Ultralytics
- OpenCV for image processing
- Dental dataset contributors

---
