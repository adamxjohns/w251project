# Setup cloud training

## Setup server
1. Install pip
```apt install python3-pip```
2. Install related packages
```
apt-get install -y libsm6 libxext6 libxrender-dev
```
3. Install related python packages
```
pip3 install mtcnn==0.1.0
pip3 install Pillow
pip3 install matplotlib
pip3 install opencv-python
pip3 install tensorflow
pip3 install --upgrade tensorflow-gpu
pip3 install --upgrade tensorboard
pip3 install keras==2.3.1
pip3 install --upgrade tensorflow-gpu==1.14.0
```
