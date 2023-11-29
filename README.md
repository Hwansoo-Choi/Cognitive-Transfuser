# Cognitive Transfuser

**Official Repository of Multimodal Data Fusion for Waypoint Prediction of Autonomous Vehicle
**



## Overview
<p align="center">
<img src="https://user-images.githubusercontent.com/62361339/201491278-f99e791f-6279-480a-b21d-086eec4838f3.gif" width="70%">
<img src="https://user-images.githubusercontent.com/62361339/201491284-60670b0e-81ad-4907-b4e5-0f44e99f4971.gif" width="70%">
<img src="https://user-images.githubusercontent.com/62361339/201491362-747d23ac-92bb-4fbd-91ab-6faa116faa46.gif" width="70%">
</p>

This is an official implementation of cognitive transfuser. Cognitive transfuser is an improved version of [transfuser]; utilizing auxiliary networks for traffic light classification and real-time semantic segmentation. The figure and table below show the overall structure and experiment results of cognitive transfuser respectively.

<p align="center">
<img src="https://user-images.githubusercontent.com/62361339/201491509-a31e31c1-960a-46d3-8c11-4e5f09faee75.png" width="70%">
</p>

<p align="center">
<img src="https://user-images.githubusercontent.com/62361339/201815232-131e6b2e-4f79-4d18-82f5-7243117b8f33.png" width="70%">
</p>


----------------------------
## Setup
<!-- #Not necessary
**Get Traffic Light Detection Module**
```bash
git clone https://github.com/sovit-123/Traffic-Light-Detection-Using-YOLOv3
mv Traffic-Light-Detection-Using-YOLOv3 Traffic_Light
wget https://drive.google.com/drive/folders/1nGRGqw5KP6js9UbXDL5G99j_jYdKgdXl?usp=sharing
```
-->
**Get requirements**
```bash
git clone https://github.com/Hwansoo-Choi/Cognitive-Transfuser/edit/Cognitive-Transfuser
conda create -n cognitive_transfuser python=3.7
conda activate cognitive_transfuser
pip3 install -r requirements.txt
```

**Get real-time semantic segmentation module**
```bash
cd ..
git clone https://github.com/MichaelFan01/STDC-Seg
```
Download pretrained model from [STDC-Seg].

Locate the STDC1-Seg and STDC2-Seg directories at
```bash
STDC-Seg/checkpoints/
```

**Setup CARLA**
```bash
chmod +x setup_carla.sh
./setup_carla.sh
```

**Get dataset**

Please refer to Dataset and Data Generation parts of [Transfuser].

**Get pretrained model**

You can download pretrained model of cognitive transfuer from [here].

Please locate the 'best_model.pth' file in **Cognitive-Transfuser/cognitive_transfuser/log/** directory.


----------------------------

## Train

```bash
cd cognitive_transfuser
python train.py
```
The trained model is saved in **cognitive_transfuser/log/**

-------------------------------

## Evaluate

**Running CARLA server**

Before running evaluation code, we must run CARLA server first.
```bash
SDL_VIDEODRIVER=offscreen SDL_HINT_CUDA_DEVICE=0 ./CarlaUE4.sh --world-port=2000 -opengl
```

**Running evaluation code**
```bash
sh /leaderboard/scripts/cognitive_transfuser_eval.sh
```

## Acknowledgement
This implementation is based on [CARLA Autopilot Leaderboard] and  [Transfuser].

Semantic segmentation module and pretrained model are from [STDC-Seg].



[Transfuser]: https://github.com/autonomousvision/transfuser/tree/cvpr2021
[transfuser]: https://github.com/autonomousvision/transfuser/tree/cvpr2021
[STDC-Seg]: https://github.com/MichaelFan01/STDC-Seg
[here]: https://drive.google.com/file/d/1jV_ne-wjptjxDaMwqFH_ItzwdbaHui-u/view?usp=share_link
[CARLA Autopilot Leaderboard]:https://github.com/carla-simulator/leaderboard.git
