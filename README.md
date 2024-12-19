Running vid2vidzero


conda create -n vid2vid_zero python=3.8 -y 
conda activate vid2vid_zero

cd  /home/youshan/Master_projects/Bharat Kathuria/VideoEdit/vid2vid-zero-main


Install the requirements.txt
Pip install -r requirements.txt

On top of this run 

pip install opencv-python xformers

/home/youshan/anaconda3/envs/vid2vid_zero/lib/python3.8/site-packages/diffusers
At this location, remove import of cached_download from dynamic_modules_utils.py file



Run get_model.ipynb cell to download the checkpoint
There are various checkpoints available or can create own

accelerate launch test_vid2vid_zero.py --config configs/car-moving.yaml
To generate output

For this, setup config at configs folder, setup the yaml file
Change parameters, give input video, prompt describing the video and expected output from prompt



========================================================================



Running TuneAVideo


conda create -n TuneAVideo python=3.8 -y 
conda activate TuneAVideo
Pip install -r requirements.txt
Pip install xformers
/home/youshan/anaconda3/envs/TuneAVideo/lib/python3.8/site-packages/diffusers
At this location, remove import of cached_download from dynamic_modules_utils.py file



accelerate launch train_tuneavideo.py --config="configs/man-skiing.yaml"
For this, setup config at configs folder, setup the yaml file
Change parameters, give input video, prompt describing the video and expected output from prompt



========================================================================

Setting up framemorph

Use the same env as vid2vidzero


conda activate vid2vid_zero
Pip install ffmpeg-python realesrgan


Under the folder -> data/videos place your videos
Under the file data/annotations.txt, give video name| description of video



!wget https://github.com/xinntao/Real-ESRGAN/releases/download/v0.1.0/RealESRGAN_x4plus.pth -P experiments/pretrained_models

No module named 'torchvision.transforms.functional_tensor'
/home/youshan/anaconda3/envs/vid2vid_zero/lib/python3.8/site-packages/basicsr/data

Change from torchvision.transforms.functional_tensor import rgb_to_grayscale
To
from torchvision.transforms.functional import rgb_to_grayscale


Python src/train.py
Python src/inference.py 	(generates videos -under results)
Python src/upscale.py         (upscales them)

====
Generating metrics

/home/youshan/Master_projects/Bharat Kathuria/VideoEdit/Metrics/Metrics.py

def save_metrics_to_csv(metrics, csv_filename="Vid2VidZeroMetrics.csv"):

Set the file name over here, and 

video_folder = '../vid2vid-zero-main/outputs/Outputs_Vid2VidZero'
Video output path over here
