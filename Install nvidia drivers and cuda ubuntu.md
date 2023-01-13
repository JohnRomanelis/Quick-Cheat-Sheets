# Removing older nvidia/cuda versions

1. Remove all files that start with nvidia in their name:

> sudo apt-get remove --purge '^nvidia-.*'

2. Remove all files that start with cuda in their name:

<sub>Purging cuda is not usually required, but it may be the solve if there are cuda leftovers that do not have nvidia in their name.</sub>

> sudo apt-get remove --purge '^cuda-.*'

3. Run the following commands:

> sudo apt-get autoclean

> sudo apt-get autoremove

# Install NVIDIA drivers - NVIDIA-SMI

1. Update the system

> sudo apt-get update

2. Install NVIDIA drivers, in this case we will install the 515 version as an example

> sudo apt install nvidia-driver-515  

3. Restart and run the following command on a terminal to test that the installation was successful

> NVIDIA-SMI


# Install CUDA

1. Go to the NVIDIA site to find all the available cuda versions https://developer.nvidia.com/cuda-toolkit-archive
2. Select the desired CUDA version (in this example 11.8) and click on the link. 
3. Add your system requirements and you will find a list of instructions to follow for the installation. 
4. Run the first 2 commands

> wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/cuda-ubuntu2004.pin

> sudo mv cuda-ubuntu2004.pin /etc/apt/preferences.d/cuda-repository-pin-600

5. The 3rd command may need superuser priviledges in some cases. If you try to run it as it is and it throws an error, you have to go and manually delete the file that has been downloaded. It is located in the default opening folder of a terminal. 

> wget https://developer.download.nvidia.com/compute/cuda/11.8.0/local_installers/cuda-repo-ubuntu2004-11-8-local_11.8.0-520.61.05-1_amd64.deb

or 

> sudo wget https://developer.download.nvidia.com/compute/cuda/11.8.0/local_installers/cuda-repo-ubuntu2004-11-8-local_11.8.0-520.61.05-1_amd64.deb

6. Run the following command. 

> sudo dpkg -i cuda-repo-ubuntu2004-11-8-local_11.8.0-520.61.05-1_amd64.deb

If it throws an error about unidentified character try writting the .deb filename yourself or simply type "cuda" and hit tap to autocomplete. 
At the end of this command it may also request to run another command (something about a key...). Just run it :P

7. Run the two following commands as in the instructions of the NVIDIA website

> sudo cp /var/cuda-repo-ubuntu2004-11-8-local/cuda-*-keyring.gpg /usr/share/keyrings/

> sudo apt-get update

8. Do NOT run the last command as suggested in the NVIDIA website as it will install the latest CUDA version and not the one you want to install. Instead you have to specify the version by adding -version at the end of the command. 

> sudo apt-get -y install cuda-11.8

9. Restart and run the following command in the terminal to test that the NVCC compiler has been successfully installed and is visible from your system. 

> nvcc -V

If it throws an error "Command 'nvcc' not found, but can be installed with: ..." You have to follow the steps in the next section to add NVCC to your path. 


# Adding NVCC to your path



# SOURCES
