# Removing older nvidia/cuda versions

Run the following to remove all files that start with nvidia in their name:

> sudo apt-get remove --purge '^nvidia-.*'

> sudo apt-get remove --purge '^cuda-.*'

***purging cuda is not usually required, but it's usefull in some cases***


