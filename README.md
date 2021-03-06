# DAIN_ESRGAN_DeOldify

The purpose of this project is to build a video processing pipeline for video frame interplation, super resolution and colorization, based on open source project [DAIN](https://github.com/baowenbo/DAIN), [ESRGAN](https://github.com/xinntao/ESRGAN) and [DEOLDIFY](https://github.com/jantic/DeOldify) and their pre-trained models. Thanks for the great work of those repos.   

It uses docker to setup runtime environment and requires GPU support. You may need to specify addtional [nvcc compilation target](https://github.com/baowenbo/DAIN/blob/0e38076069a0aa4e68a6fdbf1aa71676a16b34c0/my_package/compiler_args.py) to build [DAIN](https://github.com/baowenbo/DAIN) pytorch extension, depends on your GPU models(You can change it by patch/dain.patch). Please check nvidia [offical site](https://developer.nvidia.com/cuda-gpus). 

# How to use 
Clone the repo and it's dependecies. 
```
git clone --recursive https://github.com/iamyb/DAIN_ESRGAN_DeOldify.git
```

## Setup 
Build the docker image. It need take some time to pull all its dependencies.  
```
docker build -t dain_esrgan_deoldify .
```

Start the container (Notes: I only tested on GPU environment)  
```
docker run -itd --runtime nvidia --name dain_esrgan_deoldify --hostname ubuntu dain_esrgan_deoldify
```

Login the container  
```
docker exec -it dain_esrgan_deoldify /bin/bash
```

## Usage 
Run the example, you can check the result in folder data/output  
```
python run.py -i shanghai1937.mp4
```

If you want to test your own video, please put it into data/input/your_video.mp4 and execute:  
```
python run.py -i your_video.mp4  
```

By default, DAIN, ESRGAN and DeOldify will be processed in sequence. If you want to customize the steps, you can use '-p' parameter:
```
python run.py -i your_video.mp4 -p dain,deoldify,build
python run.py -i your_video.mp4 -p esrgan,build
```
The 'build' step here is used to combine the final frames into a video.

# Samples 
[Late Qing Dynasty(1908) History Video](https://www.bilibili.com/s/video/BV1kp4y1a77G), [Shanghai Sihang Warehouse Battle(1937) History Video](https://www.bilibili.com/video/BV1ty4y1y775)
