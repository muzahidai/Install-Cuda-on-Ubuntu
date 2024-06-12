# Install-Cuda-on-Ubuntu
Install CUDA and cudnn for Machine learning.

Install CUDA on Ubuntu Dell G7 RTX 2070

1. Install driver on software update (Driver Version: 510)
 Check which drivers are available for this device.

or, You can see list available drivers
```
ubuntu-drivers devices
```

```
sudo apt install nvidia-510*
```
 or
```
sudo ubuntu-drivers autoinstall
```
or, Install driver from GUI ..> Software Updater->Setting-> Additional drivers-> Seelct nvidia driver 510
     
Then check if the driver is installed correctly using following command. It will open a window to show drivers and GPU memories


```
nvidia-smi
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
press "i" to edit and "Esc:wq" to save
```
 blacklist nouveau
options nouvea modeset=0

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


3. Download CUDA for Linux-x86_64> Ubuntu> seelct your ununtu version>Run Local file: [[link] (https://developer.nvidia.com/cuda-11-6-0-download-archive?target_os=Linux&target_arch=x86_64&Distribution=Ubuntu&target_version=18.04&target_type=runfile_local)]

   Check ubuntu Version on your computer
   ```
   lsb_release -a 
   ```
Now Download CUDA Toolkit
   ```
  wget https://developer.download.nvidia.com/compute/cuda/11.8.0/local_installers/cuda_11.8.0_520.61.05_linux.run
   ```

5. Install CUDA_toolkit_11.8  // Download the exact cuda version that you want to install, we are doing cuda 11.8
Allow read and write permission to cudafile.run
```
sudo chmod 777 cuda_11.8.0_520.61.05_linux.run
```
Install   
```
sudo sh cuda_11.8.0_520.61.05_linux.run
``` 

4.1.Follow the instructions, accpet and agree all yes, except do not install the driver (uncheck driver by pressing enter on it, because we already installed nvidia driver previously)

4.2. Export path: change the directory name of "/cuda-xx.x/bins$" according to yours. You can go to the directory manually to see the exact name.

```
sudo vim ~/.bashrc
```
>>press i to edit the file and addd the following lines inside the file at the bottom. Change cuda directory according to you, "/usr/local/cuda-1x.x/bin'. To make sure, you can manually go this directory and see the directory name to be confirmed.
```
export PATH=/usr/local/cuda-11.8/bin${PATH:+:${PATH}}  
export LD_LIBRARY_PATH=/usr/local/cuda-11.8/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
```
>>press esc > : > wq >enter
```
source ~/.bashrc
```
4.3 #Check cuda compiler: it will output: Cuda compilation tools, release 10.0, V10.0.130
```
nvcc --version   
```
or
```
nvcc -V
```
If it is installed correctly it will Output: Cuda compilation tools, release 11.8, V11.8.89

5. Now download the CUDNN library | Register and account then u get full access. We are downloading Download cuDNN v8.9.7 (December 5th, 2023), for CUDA 11.x. you can download based on your demand

6. Select ubuntu version and debian file on [[Link]( https://developer.nvidia.com/rdp/cudnn-archive)]
                                                 

			Download Manually by clicking:

		                 i. Local Installer for Ubuntu18.04 x86_64 (Deb)
   It will download following file: cudnn-local-repo-ubuntu1804-8.9.7.29_1.0-1_amd64.deb
	         		

8. Install this files, and change the file name according to yours

```
sudo dpkg -i cudnn-local-repo-ubuntu1804-8.9.7.29_1.0-1_amd64.deb
```

CUDA setup has been Finished...

8.Now do check if cuda is working or not-> run a digit classification test. Download cudav8 samples from github.


Copy cuda samples directories (cudnn_samples_v8) and paste to /usr/local/cuda-11.8

>> cp -r [source/cudnn_samples_v7/}  [destination/usr/local/cuda-10.0/}
Example
```
sudo cp -r /usr/src/cudnn_samples_v8/ /usr/local/cuda-11.8/
```
Change the current directory to sudnn samples directory
```
cd /usr/local/cuda-11.8/cudnn_samples_v7/mnistCUDNN/
```
```
make clean
make
```

8.1 Perform classification

```
./mnistCUDNN    
```				
 Output: 
	Result of classification: 1 3 5

	Test passed!

 8.2 If cudnn.h file not found during make or performing classification test
```
sudo apt-get install libcudnn8-dev  
```
If FreeImage is not set up correctly during performing classification test
```
sudo apt-get install libfreeimage3 libfreeimage-dev    
```
Now perform classification again, repeat 8.1
***************************************************************************
It's Done

**************************************************************************
How to remove cudatoolkit and install other version
**************************************************************************

9. First remove cuda toolkit or delete the folder cuda-11.8 on /usr/local

Uninstall:cuda-uninstaller in /usr/local/cuda-11.0/bin
```
cd /usr/local/cuda11.8/bin
sudo ./uninstall_cuda_11.8.pl
```
or, Delete the cuda folder and subfolders
```
sudo rm -rf /usr/local/cuda**
reboot
```
If you install new version of cuda, follow instruction from step 3 to 8.2

**************************************************************************
Install anaconda and tensorflow-gpu
**************************************************************************
10. First Install Anaconda 2023.03 version then install tensorflow GPU

