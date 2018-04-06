# install opencv3.4 Python3.6 -Raspberry Pi3 
1. Raspberry Pi 3 B +
Raspbian Stretch, version March 2018 
2. Install Python3.6

$wget https://www.python.org/ftp/python/3.6.2/Python-3.6.2.tar.xz
$tar xf Python-3.6.2.tar.xz
$cd Python-3.6.2
$./configure --enable-optimizations
$make
$sudo make altinstall
$rm Python-3.6.2.tar.xz
--
3. Expand filesystem
$ sudo raspi-config

--And then select the “Advanced Options” menu item
--Select “Expand filesystem”
--and reboot pi
$ sudo reboot

4. Install dependencies
$ sudo apt-get update && sudo apt-get upgrade
$ sudo apt-get install build-essential cmake pkg-config
$ sudo apt-get install libjpeg-dev libtiff5-dev libjasper-dev libpng12-dev
$ sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev
$ sudo apt-get install libxvidcore-dev libx264-dev
$ sudo apt-get install libgtk2.0-dev libgtk-3-dev
$ sudo apt-get install libatlas-base-dev gfortran

5. Download OpenCV3.4 source code 
$cd ~
$wget -O opencv.zip https://github.com/Itseez/opencv/archive/3.4.0.zip
$unzip opencv.zip
$wget -O opencv_contrib.zip https://github.com/Itseez/opencv_contrib/archive/3.4.0.zip
$unzip opencv_contrib.zip

6. Install virtualenv and virtualenvwrapper
$sudo pip3.6 install virtualenv virtualenvwrapper
$ sudo rm -rf ~/.cache/pip

7. Update profile for virtualenv and virtualenvwrapper
-- virtualenv and virtualenvwrapper
$ export WORKON_HOME=$HOME/.virtualenvs
$source /usr/local/bin/virtualenvwrapper.sh

8. Create Python3.6 on virtual environment 
$ source ~/.profile
$ mkvirtualenv cv -p python3.6

9. Run cv
$ workon cv
-- you can see in the terminal: (cv)pi@hng_pi: -$
--and try:
(cv)pi@hng_pi: -$python
-- you can see the version of python is running :
Python 3.6.2

10. install setuptools, dev, Numpy
$sudo pip3.6 install numpy
$sudo pip3.6 install setuptools 
$sudo pip3.6 install dev 

11. Compile and Install OpenCV3.4 for Python3.6
$ cd ~/opencv-3.4.0/
$ mkdir build
$ cd build
$ cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D INSTALL_PYTHON_EXAMPLES=ON  -D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib-3.4.0/modules  -D BUILD_EXAMPLES=ON 
 

12. Swap Space size before compiling to add more virtual memory 
$sudo nano /etc/dphys-swapfile
--open and edit CONF_SWAPSIZE, change it 

--# CONF_SWAPSIZE=100
CONF_SWAPSIZE=1024

-- save it and exit
-- test
$sudo /etc/init.d/dphys-swapfile stop
$sudo /etc/init.d/dphys-swapfile start

13. Finally ready to be Compile

$make -j4

14. Install the build on raspberry pi 
$sudo make install 
$sudo ldconfig 

15. Finish installing OpenCV3.4.0 on Raspberry Pi3 B+
$ ls -l /usr/local/lib/python3.6/site-packages/
$ cd /usr/local/lib/python3.6/site-packages/
-- you can see file:
cv2.cpython-36m-arm-linux-gnueabihf.so
-- we need to rename this file to cv2.so
$ sudo mv cv2.cpython-36m-arm-linux-gnueabihf.so cv2.so

16. Tesing cv2
$python3.6 
>>>import cv2

17. Change your SWAPSIZE back 

CONF_SWAPSIZE=100
--# CONF_SWAPSIZE=1024

$ sudo /etc/init.d/dphys-swapfile stop
$ sudo /etc/init.d/dphys-swapfile start

18. Clean up your house-- make sure cv2 already installed 
$ cd ~
$ rm -rf opencv-3.4.0 opencv_contrib-3.4.0
$ rm opencv.zip opencv_contrib.zip

# Good luck


