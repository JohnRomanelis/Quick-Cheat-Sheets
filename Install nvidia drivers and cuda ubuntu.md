*For Ubuntu 22.04 and CUDA 11.8 check this link: https://gist.github.com/MihailCosmin/affa6b1b71b43787e9228c25fe15aeba*

# Removing older nvidia/cuda versions

1. Remove all files that start with nvidia in their name:

> sudo apt-get remove --purge '^nvidia-.*'

2. Remove all files that start with cuda in their name:

<sub>Purging cuda is not usually required, but it may be the solve if there are cuda leftovers that do not have nvidia in their name.</sub>

> sudo apt-get remove --purge '^cuda-.*'

3. Run the following commands:

> sudo apt-get autoclean

> sudo apt-get autoremove

4. Extra: 

- If you go to the */var* directory you can find all the installed cuda versions. If you delete a cuda version there may be leftovers in this directory that take a lot of free space of the disk. 
- If you go to the */home/username/* directory there may also be leftover *.deb* files that you can delete. Check for these files after you finish the CUDA installation anyway to free up some space. 

# Install NVIDIA drivers - NVIDIA-SMI

1. Update the system

> sudo apt-get update

2. Install NVIDIA drivers, in this case we will install the 515 version as an example

> sudo apt install nvidia-driver-515  

3. Restart the computer and run the following command on a terminal to test that the installation was successful

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

If it throws an error about unidentified character, try writting the .deb filename yourself or simply type "cuda" and hit tap to autocomplete. 
At the end of this command it may also request to run another command (something about a key...). Just run it and skip the next command in the NVIDIA instructions. Else just run the following command as described: 

> sudo cp /var/cuda-repo-ubuntu2004-11-8-local/cuda-*-keyring.gpg /usr/share/keyrings/

7. Update the system 

> sudo apt-get update

8. Do NOT run the last command as suggested in the NVIDIA website as it will install the latest CUDA version and not the one you want to install. Instead you have to specify the version by adding -version at the end of the command. 

> sudo apt-get -y install cuda-11.8

9. Restart the computer and run the following command in the terminal to test that the NVCC compiler has been successfully installed and is visible from your system. 

> nvcc -V

If it throws an error "Command 'nvcc' not found, but can be installed with: ..." You have to follow the steps in the next section to add NVCC to your path. 


# Adding NVCC to your path

1. From a terminal run:

> nano /home/username/.bashrc 

2. Inside there add the following: (Change 11.8 with your preferred version)

 > export PATH="/usr/local/cuda-11.8/bin:$PATH"
 
 > export LD_LIBRARY_PATH="/usr/local/cuda-11.8/lib64:$LD_LIBRARY_PATH"

3. Hit ***ctrl + o*** to save the changes and press enter or return key to accept. Then hit ***ctrl + x*** to close the editor. 

4. Run 

> source .bashrc 

5. On a new terminal (may work on the same terminal as well), run: 

> nvcc -V 

The nvcc version should be displayed at the terminal. 


# SOURCES
- https://askubuntu.com/questions/885610/nvcc-version-command-says-nvcc-is-not-installed

- https://developer.nvidia.com/cuda-11-8-0-download-archive?target_os=Linux&target_arch=x86_64&Distribution=Ubuntu&target_version=20.04&target_type=deb_local
