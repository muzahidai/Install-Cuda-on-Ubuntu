# Install-Cuda-on-Ubuntu
Install CUDA and cudnn for Machine learning.

 Install CUDA on Ubuntu Dell G7 RTX 2070

1. Install driver on software update (Driver Version: 470.182.03)
 Check which drivers are available for this device
>> ubuntu-drivers devices       // u can see list available drivers
>>sudo apt install nvidia-34*
 or
```
sudo ubuntu-drivers autoinstall
```
or, Install driver GUI ..> setup-> additional drivers
     
Then check if the driver is installed correctly. It will open a window to show drivers and GPU memories


``` nvidia-smi  
```
  
1.1 Choose NVIDIA for graphics-display and block nouvea

Check whether nvidia or who is being used for display
 ```
 lsmod | grep nouvea
```
if there is an output means nouvea is being used, need to block it
 ```
sudo vim /etc/modprobe.d/blacklist.conf
```
```
>press i  // edit
      blacklist nouveau
       options nouvea modeset=0
   >Esc:wq     // save and quit
```

```
sudo update initramfs -U
```
```
sudo reboot
```

Now check again
```
lsmod | grep nouvea
```

2. Install Dependencies & pre-requisites

```
sudo apt install build-essential
sudo apt install gcc tar make git
sudo apt-get install freeglut3-dev build-essential libx11-dev libxmu-dev libxi-dev libgl1-mesa-glx libglu1-mesa libglu1-mesa-dev
```
If cudnn.h file not found during testing cuda
```
sudo apt-get install libcudnn8-dev  
```
If FreeImage is not set up correctly during testing cuda
```
sudo apt-get install libfreeimage3 libfreeimage-dev    
```

3. Download CUDA: [[link]https://(developer.nvidia.com/cuda-10.0-download-archive?target_os=Linux&target_arch=x86_64&target_distro=Ubuntu&target_version=1804&target_type=runfilelocal)]

4. Install CUDA_toolkit_10.0  // Download the exact cuda version that you want to install, we are doing cuda 10.0

chmod 777 cuda_10.0.130_410.48_linux.run    // allow read and write permission
>>sudo ./cuda_10.0.130_410.48_linux.run       // install
 
4.1.Follow the instructions, accpet and agree all yes, except do not install the driver (uncheck driver by pressing enter on it, because we already installed nvidia driver previously)

5. Now download the CUDNN library | Register and account then u get full access. We are downloading cudnnv7.6.5. you can download based on your demand

6. Download the following three files on [[Link]( https://developer.nvidia.com/rdp/cudnn-archive)]
                                                 

			Download Manually:

		                 i. cuDNN Runtime Library for Ubuntu20.04 x86_64 (Deb)
	         		ii. cuDNN Developer Library for Ubuntu20.04 x86_64 (Deb)
	         		iii. cuDNN Code Samples and User Guide for Ubuntu20.04 x86_64 (Deb)

7.1 Install these three files, and change the file name according to yours

```
sudo dpkg -i libcudnn7_7.6.5.32-1+cuda10.0_amd64.deb
```
```
sudo dpkg -i libcudnn7-dev_7.6.5.32-1+cuda10.0_amd64.deb
```
```
sudo dpkg -i libcudnn7-doc_7.6.5.32-1+cuda10.0_amd64.deb
```

8. Export path: change the directory name of "/cuda-xx.x/bins$" according to yours. You can go to the directory manually to see the exact name.

```
sudo vim ~/.bashrc
```
        >>press i
         >>export PATH=/usr/local/cuda-10.0/bin${PATH:+:${PATH}}  
         >>export LD_LIBRARY_PATH=/usr/local/cuda-10.0/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
	 >>press esc > : > wq >enter
```
source ~/.bashrc
```
........CUDA setup has been Done...

8.1 #Check cuda compiler: output: Cuda compilation tools, release 10.0, V10.0.130
```
nvcc --version   
```
9.Now do check if cuda is working- run a digit classification test


Copy cuda samples directories (cudnn_samples_v7) and paste to /usr/local/cuda-10.x.x  

>> cp -r [source/cudnn_samples_v7/}  [destination/usr/local/cuda-10.0/}
Example
```
sudo cp -r /usr/src/cudnn_samples_v7/ /usr/local/cuda-10.0/
```

```
cd /usr/local/cuda-10.0/cudnn_samples_v7/mnistCUDNN/
```
```
make clean
```
```
make
```
Perform classification

```
./mnistCUDNN    
```				
 Output: 
	Result of classification: 1 3 5

	Test passed!
***************************************************************************
It's Done



