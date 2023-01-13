# Removing older nvidia/cuda versions

Run the following command to remove all files that start with nvidia in their name:

> sudo apt-get remove --purge '^nvidia-.*'

Run the following command to remoce all files that start with cuda in their name:

<sub>Purging cuda is not usually required, but it may be the solve if there are cuda leftovers that do not have nvidia in their name.</sub>

> sudo apt-get remove --purge '^cuda-.*'

Run the following commands:

> sudo apt-get autoclean
> sudo apt-get autoremove


