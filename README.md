# Vid2Vid-Zero Setup and Execution

### Environment Setup
```bash
# Create and activate the conda environment
conda create -n vid2vid_zero python=3.8 -y
conda activate vid2vid_zero
```

### Install Dependencies
```bash
# Navigate to the project directory
cd /home/youshan/Master_projects/Bharat\ Kathuria/VideoEdit/vid2vid-zero-main

# Install dependencies from requirements.txt
pip install -r requirements.txt

# Additional dependencies
pip install opencv-python xformers
```

### Modify Diffusers File
Navigate to the following location:
```bash
/home/youshan/anaconda3/envs/vid2vid_zero/lib/python3.8/site-packages/diffusers
```
Edit the file `dynamic_modules_utils.py` and **remove** the import of `cached_download`.

### Download Checkpoints
Run the `get_model.ipynb` notebook to download the required checkpoints. You can use pre-existing checkpoints or create your own.

### Generate Output
```bash
# Run the script to generate output
accelerate launch test_vid2vid_zero.py --config configs/car-moving.yaml
```

#### Configuration Setup
1. Navigate to the `configs` folder.
2. Set up the YAML file (e.g., `car-moving.yaml`).
3. Update the following parameters:
   - Input video path
   - Prompt describing the video
   - Expected output description

---

# Tune-A-Video Setup and Execution

### Environment Setup
```bash
# Create and activate the conda environment
conda create -n TuneAVideo python=3.8 -y
conda activate TuneAVideo
```

### Install Dependencies
```bash
# Install dependencies from requirements.txt
pip install -r requirements.txt

# Additional dependencies
pip install xformers
```

### Modify Diffusers File
Navigate to the following location:
```bash
/home/youshan/anaconda3/envs/TuneAVideo/lib/python3.8/site-packages/diffusers
```
Edit the file `dynamic_modules_utils.py` and **remove** the import of `cached_download`.

### Train the Model
```bash
# Launch the training script
accelerate launch train_tuneavideo.py --config="configs/man-skiing.yaml"
```

#### Configuration Setup
1. Navigate to the `configs` folder.
2. Set up the YAML file (e.g., `man-skiing.yaml`).
3. Update the following parameters:
   - Input video path
   - Prompt describing the video
   - Expected output description

---

# FrameMorph Setup and Execution

### Environment Setup
Use the same environment as Vid2Vid-Zero:
```bash
conda activate vid2vid_zero
pip install ffmpeg-python realesrgan
```

### Data Preparation
1. Place your videos under the folder `data/videos`.
2. Add video descriptions to `data/annotations.txt` using the following format:
   ```
   video_name | description of video
   ```

### Download Pretrained Model
```bash
# Download Real-ESRGAN pretrained model
!wget https://github.com/xinntao/Real-ESRGAN/releases/download/v0.1.0/RealESRGAN_x4plus.pth -P experiments/pretrained_models
```

### Modify Basicsr File
Navigate to the following location:
```bash
/home/youshan/anaconda3/envs/vid2vid_zero/lib/python3.8/site-packages/basicsr/data
```
Edit the file to change the import:
```python
# Replace this line
from torchvision.transforms.functional_tensor import rgb_to_grayscale

# With this line
from torchvision.transforms.functional import rgb_to_grayscale
```

### Train and Inference
```bash
# Train the model
python src/train.py

# Generate videos
python src/inference.py

# Upscale videos
python src/upscale.py
```
- Generated videos are saved under the `results` folder.

---

# Generating Metrics

### Metrics Evaluation
Navigate to:
```bash
/home/youshan/Master_projects/Bharat\ Kathuria/VideoEdit/Metrics/Metrics.py
```

### Update File Paths
1. Set the CSV file name in the function `save_metrics_to_csv`:
   ```python
   def save_metrics_to_csv(metrics, csv_filename="Vid2VidZeroMetrics.csv"):
   ```
2. Update the video folder path:
   ```python
   video_folder = '../vid2vid-zero-main/outputs/Outputs_Vid2VidZero'
   ```

Run the script to evaluate metrics and save them to a CSV file.
