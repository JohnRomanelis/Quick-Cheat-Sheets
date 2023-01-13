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

2. Install drivers

> sudo apt install nvidia-driver-515  # 515 is an example, can be replaced with any other version


