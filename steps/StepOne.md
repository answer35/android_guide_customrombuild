#Set Up a Build Environment

* A) The Way I do..


```bash

#First update/upgrade of hte new virtual machine
sudo apt update
sudo apt -y upgrade

#Install Python 3.7
sudo apt install software-properties-common
sudo add-apt-repository ppa:deadsnakes/ppa -y
sudo apt update
sudo apt install -y python3.7

#Install Git
sudo apt install git-core

#Install SSHPass if needed
sudo apt install sshpass

#Configure Git
git config --global user.email $email
git config --global user.name "$username"

#Configure SSHPass
ssh $sfusername@frs.sourceforge.net

#Install all components required for building environement (Thanks to Akhil Narang <me@akhilnarang.dev>)
git clone https://github.com/akhilnarang/scripts
cd scripts
sudo bash setup/android_build_env.sh

#Configuring swap for building

#Checking the System for Swap Information
sudo swapon --show
free -h

#Checking Available Space on the Hard Drive Partition
df -h

#Creating a Swap File
sudo fallocate -l 16G /swapfile
ls -lh /swapfile

#Enabling the Swap File
sudo chmod 600 /swapfile
ls -lh /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
sudo swapon --show
free -h

#Making the Swap File Permanent
sudo cp /etc/fstab /etc/fstab.bak
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
```

* B) The AOSP way to do..

https://source.android.com/setup/build/initializing
