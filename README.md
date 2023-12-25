# How to Install CUDA on Linux (Ubuntu) RTX2060 #
- NVIDIA-Linux-x86_64-535.146.02.run file from [NVIDIA's website](https://www.nvidia.com/download).

- Edit or create file named blacklist-nouveau.conf in /etc/modprobe.d/ :
  - `blacklist nouveau`
  - `options nouveau modeset=0`

- regenerate the kernel initramfs:
  - `sudo update-initramfs -u`

- reboot

### Boot into Text Mode ###

- To install the driver, you should stop the graphical interface (X server). You can do this by booting into text mode.

- Reboot your system and open the GRUB menu by pressing Shift or Esc during boot-up.
- Select the option to edit your boot parameters, usually by pressing e.
- Find the line that starts with linux and add 3 at the end of this line. This will boot your system into runlevel 3 (multi-user text mode).
- Press Ctrl + X or F10 to boot.
  
- Navigate to the Driver File: Change directory to where you have downloaded the .run file:
- cd /Downloads/

- `chmod +x NVIDIA-Linux-x86_64-535.146.02.run`

- `sudo ./NVIDIA-Linux-x86_64-535.146.02.run`

- `sudo reboot`

- verify: `nvidia-smi`


## Installing the CUDA Toolkit for Linux ##

- `sudo apt-get install zlib1g`

 ### Downloading cuDNN for Linux ###

In order to download cuDNN, ensure you are registered for the [NVIDIA Developer Program](https://developer.nvidia.com/accelerated-computing-developer).
Go to: NVIDIA [cuDNN](https://developer.nvidia.com/cudnn) home page.
Click Download. (CUDA 12 better)

Debian Local Installation:
`sudo dpkg -i cudnn-local-repo-$distro-8.x.x.x_1.0-1_amd64.deb`
 
Import the CUDA GPG key.
`sudo cp /var/cudnn-local-repo-*/cudnn-local-*-keyring.gpg /usr/share/keyrings/`

Refresh the repository metadata.
`sudo apt-get update`

Install the runtime library.
`sudo apt-get install libcudnn8=8.x.x.x-1+cudaX.Y`

Install the developer library.
`sudo apt-get install libcudnn8-dev=8.x.x.x-1+cudaX.Y`

Install the code samples.
`sudo apt-get install libcudnn8-samples=8.x.x.x-1+cudaX.Y`

### Verifying the Installation ###

Copy the cuDNN samples to a writable path.
`cp -r /usr/src/cudnn_samples_v8/ $HOME`

Go to the writable path.
`cd  $HOME/cudnn_samples_v8/mnistCUDNN`

Compile the mnistCUDNN sample.
`make clean && make`

Run the mnistCUDNN sample.
`./mnistCUDNN`
