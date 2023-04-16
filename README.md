# Cotton-robot

## Hardware

1. Jetson nano
2. SD card  64 gb minimum required
3. Card reader
4. PC
5. Internet Connectivity
6. Wifi dongle for jetson nano 
           
           
## Installation guide

### Steps
1. Burning the jetson image in sd card using PC
2. Install Dependencies 
3. Install Realsense Package
4. Install Opencv
5. Install Tensorflow
6. Install NoMachine

## 1. Burning the jetson image in sd card using PC (Jetpack)(4.4.1)

Download the image from below link(required space is 6 gb to 7gb)(jetson-nano-jp441-sd-card-image)

https://drive.google.com/drive/folders/1K_XHoWKTxhmEQ-kiTfzmiqMf2MNlc0hB?usp=sharing

#### Instruction to Write Image to the microSD Card 

1. Download(from above link), install, and launch (SD Card Formatter 5.0.2 Setup EN) for Windows.
2. Select card drive
3. Select “Quick format”
4. Leave “Volume label” blank
5. Click “Format” to start formatting, and “Yes” on the warning dialog

#### Use Etcher to write the Jetson Nano Developer Kit SD Card Image to your microSD card

1. Download(from above link), install, and launch (balenaEtcher-Setup-1.7.9).
2. Click “Select image” and choose the zipped image file downloaded earlier.
3. Insert your microSD card if not already inserted.
4. Click “Select drive” and choose the correct device.
5. Click “Flash!” It will take Etcher about 10 minutes to write and validate the image if your microSD card is connected via USB3.
6. After Etcher finishes, Windows may let you know it doesn’t know how to read the SD Card. Just click Cancel and remove the microSD card.

After your microSD card is ready, proceed to set up your developer kit.

### Setup your Jetson Nano
1. Insert the SD card to Jetson Nano.
2. Connect the cooling fan to heat sink.
3. Place the jetson Nano on Electro Static Mat.
4. Connect the power supply.
5. Connect WiFi Dongle, Mouse and Keyboard to the USB port.
6. Connect the Monitor to the jetson nano.
7. Create Username And Password.

## NEVER RUN THIS COMMAND IN ANY CONDITION
```
sudo apt-get update
sudo apt-get upgrade
```
## 2. Install Dependicies (connect wifi on jetson  nano  using wifi dongle (internet required))

Open terminal in jetson nano in Home Directory

## To run all core of Jetson nano
```
sudo nvpmodel -m 0
sudo jetson_clocks
```
## To Start Jetson Fan
Download and Unzip the "jetson-fan-ctl-master.zip" file from below link in Home Directory

https://drive.google.com/drive/folders/1K_XHoWKTxhmEQ-kiTfzmiqMf2MNlc0hB?usp=sharing

### Open terminal in "jetson-fan-ctl-master" folder
```
sudo ./install.sh
```
### Open terminal in jetson nano and Install all dependency in Home Directory
1. Install Python (Version 3.6.9)
```
sudo apt update
sudo apt-get install python python3.6
sudo apt-get install gedit
sudo apt-get install -y python3-pip
```
2. Install pyserial
```
pip3 install pyserial
```
3. Install i2c
```
pip3 install smbus
```
4. Install Cython
```
pip3 install setuptools wheel cython

```
5. Install Pandas(1.1.5)
(Download Source Distribution from the link pandas-1.1.5.tar.gz -> Extract -> open the folder ->)

https://drive.google.com/drive/folders/1K_XHoWKTxhmEQ-kiTfzmiqMf2MNlc0hB?usp=sharing

Open the Terminal in the folder

```
sudo python3 setup.py install
```

6. Install openpyxl(3.0.10)

https://drive.google.com/drive/folders/1K_XHoWKTxhmEQ-kiTfzmiqMf2MNlc0hB?usp=sharing

Open the Terminal in the folder
```
pip3 install openpyxl-3.0.10-py2.py3-none-any.whl
pip3 install --upgrade xlrd

```
7. Install Remaining Dependencies
```
sudo apt-get install -y nano curl
sudo apt-get install -y python3-pip python3-dev python3-setuptools
sudo apt-get install -y libcanberra-gtk0 libcanberra-gtk-module
sudo apt install protobuf-compiler libprotoc-dev
```
## 3. Install Realsense Package(2.49)
(Install in Home Directory)

https://drive.google.com/drive/folders/1K_XHoWKTxhmEQ-kiTfzmiqMf2MNlc0hB?usp=sharing


Extract the librealsense-2.49.0.zip  file in Home Directory.

The file will be extracted in realsense2.49 folder.

#### Open the realsense2.49 folder and open the terminal.
#### KERNEL PATCH FOR BETTER PERFORMANCE AND COMPATIBILITY AND GETTING METADATA
```
./scripts/patch-realsense-ubuntu-L4T.sh  
```

### Open Terminal
```
mkdir build
cd build
sudo apt-get install curl
sudo apt-get install libssl-dev libcurl4-openssl-dev
sudo apt install protobuf-compiler libprotoc-dev
```
### open bash.rc file
```
 sudo gedit ~/.bashrc
```
### Add Cuda Path at end and save
```
 export CUDA_HOME=/usr/local/cuda
 export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib64:/usr/local/cuda/extras/CUPTI/lib64
 export PATH=$PATH:$CUDA_HOME/bin
```
## Restart Jetson Nano
### Install Dependencies(Open the realsense2.49 folder -->> open build folder and open the terminal)
```
sudo apt-get install libxinerama-dev
sudo apt-get install libxcursor-dev
pip3 install Cython
sudo apt-get install python3 python3-dev
```

### To compile
```
cmake ../ -DBUILD_PYTHON_BINDINGS:bool=true -DFORCE_RSUSB_BACKEND=false -DPYTHON_EXECUTABLE=/usr/bin/python3 -DBUILD_WITH_CUDA:bool=true
```
In build Directory.
```
make -j4
```
This will take 4 to 6 hours 
```
sudo make install

```
### Open Bash.rc file
```
sudo gedit ~/.bashrc
```
### Add following path at end and save

```
export PATH=$PATH:~/.local/bin
export PYTHONPATH=$PYTHONPATH:/usr/local/lib
export PYTHONPATH=$PYTHONPATH:/usr/local/lib/python3.6/pyrealsense2
```
### Restart the Jetson nano
Check the installation in Jetson nano by using terminal  
```
python3
import pyrealsense2
```
#### If the above command gives no error then continue otherwise delete the build folder in realsense2.49 and start from step 3 open terminal.
     
### Debian Installation (open terminal in home directory)
```
sudo apt-key adv --keyserver keys.gnupg.net --recv-key F6E65AC044F831AC80A06380C8B3A55A6F3EFCDE || sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-key F6E65AC044F831AC80A06380C8B3A55A6F3EFCDE
sudo add-apt-repository "deb https://librealsense.intel.com/Debian/apt-repo bionic main" -u
```
### SDK Installation (open terminal in home directory)
```
sudo apt-get install librealsense2-utils
sudo apt-get install librealsense2-dev
```
## 4. Install Opencv (open terminal in home directory)
```
sudo apt-get install python3-opencv
```
## 5. Install Tensorflow (open terminal in home directory)
```
sudo apt-get install libhdf5-serial-dev hdf5-tools libhdf5-dev zlib1g-dev zip
sudo apt-get install libjpeg8-dev liblapack-dev libblas-dev gfortran
sudo pip3 install -U pip testresources setuptools==49.6.0
sudo pip3 install -U --no-deps numpy==1.19.4 future==0.18.2 mock==3.0.5  keras_preprocessing==1.1.2 keras_applications==1.0.8 
```
### Restart the Jetson Nano
(open terminal in home directory)
```
pip3 install pkgconfig
sudo env H5PY_SETUP_REQUIRES=0 pip3 install -U --no-build-isolation h5py==3.1.0
```
#### If there is error (No module name 'Cython')

 use the following command

```
sudo ln -s /usr/include/locale.h /usr/include/xlocale
pip3 install h5py==3.1.0
```
#### no error then continue
### Install Tensorflow
```
sudo pip3 install --pre --extra-index-url https://developer.download.nvidia.com/compute/redist/jp/v44  'tensorflow<2'
```
### Install tensorrt_demos for using jyosh model tensorrt

Clone JK Jung  github directory
```
 mkdir project 
 cd project
 git clone https://github.com/jkjung-avt/tensorrt_demos.git
```
 
### Now this repository has been cloned at "${HOME}/project/tensorrt_demos", follow these steps

#### Install Pycuda(2019.1.2)(open terminal in home directory)
```
 cd ${HOME}/project/tensorrt_demos/yolo
 ./install_pycuda.sh
```
#### Install Onyx(1.9.0)
```
sudo pip3 install onnx==1.9.0
```
#### Build Yolo layer plugin
When done, a "libyolo_layer.so" would be generated
```
cd ${HOME}/project/tensorrt_demos/plugins
make
```
#### Communication Between Jetson nano and STM (open terminal in home directory)
```
systemctl stop nvgetty
systemctl disable nvgetty
udevadm trigger
sudo apt-get install python3-serial
sudo pip3 install Jetson.GPIO
```
## 6. Install NoMachine
```
wget https://www.nomachine.com/free/arm/v8/deb -O nomachine.deb
sudo dpkg -i nomachine.deb
```














