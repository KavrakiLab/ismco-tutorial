# Current methods and open challenges for structural modeling in cancer immunotherapy - ISMCO'20

Welcome to the second edition of the [ISMCO'20](http://ismco.net/) tutorial on [Current methods and open challenges for structural modeling in cancer immunotherapy](http://ismco.net/index.php/tutorials-2/)!!!

## Tentative outline

| Activity | Duration (m) | Time (PST) |
|----------|:-------------:|:-------------:|
| Opening  | 5 | **3:00** |
| Cellular immunity for cancer immunotherapy | 15 | - |
| Exploring [IEDB](https://www.iedb.org/) resources (live demo)	| 40 | - |
| **Break**	| **15** | **4:00** |
| Downloading structures from [PDB](https://www.rcsb.org/)	| 5 | **4:15** |
| Visualizing pHLA structures w Chimera (live)	| 30 | - |
| **Break**	| **15** | **4:50** |
| Intro to pHLA modeling |	10 | **5:05** |
| DINC ([webserver](http://dinc.kavrakilab.org/) live demo) |	8 | - |
| DockTope ([webserver](http://tools.iedb.org/docktope/) live demo) |	8 | - |
| Intro to Jupyter notebooks (live demo) |	8 | - |
| **Break**	| **15** | **5:25** |
| Intro to HLA-Arena	| 10 | **5:40** |
| HLA-Arena workflow 0 (Ape-Gen)	| 10 | - |
| HLA-Arena workflow 1 (DINC)	| 15 | - |
| HLA-Arena workflow 3 (mhcflurry + APE-Gen) |	30 | - |
| Conclusion | - | **19:00** |


## Software requirements

 You will need to install the following programs **PRIOR TO THE BEGINNING OF THE TUTORIAL**! This is important since the download of some of the packages could take hours depending on your internet connection. We will not be able to help you with the installation during the tutorial.

If you have any questions about the installation, please contact mmr9@rice.edu.

### 1. Softwares that need to be installed:

#### 1.1 UCSF Chimera
If you have Microsoft Windows, click [here](https://www.cgl.ucsf.edu/chimera/cgi-bin/secure/chimera-get.py?file=win64/chimera-1.14-win64.exe) to download and here(https://www.cgl.ucsf.edu/chimera/data/downloads/1.14/win64.html) to follow the instructions on how to install

If you have Mac OS X, click [here](https://www.cgl.ucsf.edu/chimera/cgi-bin/secure/chimera-get.py?file=mac64/chimera-1.14-mac64.dmg) to download and [here](https://www.cgl.ucsf.edu/chimera/data/downloads/1.14/mac64.html) to follow the instructions on how to install

If you have Linux, click [here](https://www.cgl.ucsf.edu/chimera/cgi-bin/secure/chimera-get.py?file=linux_x86_64/chimera-1.14-linux_x86_64.bin) to download and [here](https://www.cgl.ucsf.edu/chimera/data/downloads/1.14/linux_x86_64.html) to follow the instructions on how to install

#### 1.2. Jupyter notebook
You can install Jupyter notebook using pip3 or via Anaconda.
1.2.1. Pip3 installation: open a Terminal window and type:

        pip3 install notebook

1.2.2. To install via Anaconda follow innstrcutions on this link:
[https://swcarpentry.github.io/python-novice-inflammation/setup/index.html](https://swcarpentry.github.io/python-novice-inflammation/setup/index.html)

#### 1.2.3. If you have Windows, follow the instructions on this link:
[https://www.geeksforgeeks.org/how-to-install-jupyter-notebook-in-windows/](https://www.geeksforgeeks.org/how-to-install-jupyter-notebook-in-windows/)

To test if your installation was successfull, type jupyter-notebook or jupyter notebook in the terminal. You should expect a browse opening. If you install via Anaconda you might have to first activate the conda environment in which you installed Jupyter Notebook. You should also be able to start Jupyter Notebook from the Anaconda Navigator.

#### 1.3. HLA-Arena
First, you will need to install Docker, unless you already have it. For that, follow the instructions in one of these links:

        Docker for Mac or Windows: https://www.docker.com/products/docker-desktop
        Docker for Linux: https://docs.docker.com/install

Next, in a command prompt, pull the HLA-Arena image from Docker Hub by typing:

        docker pull kavrakilab/hla-arena

This step can take hours and it will require about 20 Gb of disk space.


### 2. Checking your installation:

#### 2.1. Test your Docker installation:
In the command line (or prompt) run the following command:

          docker run hello-world

You should see the following output:

        Hello from Docker!
        This message shows that your installation appears to be working correctly.

        To generate this message, Docker took the following steps:
         1. The Docker client contacted the Docker daemon.
         2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
            (amd64)
         3. The Docker daemon created a new container from that image which runs the
            executable that produces the output you are currently reading.
         4. The Docker daemon streamed that output to the Docker client, which sent it
            to your terminal.

        To try something more ambitious, you can run an Ubuntu container with:
         $ docker run -it ubuntu bash

        Share images, automate workflows, and more with a free Docker ID:
         https://hub.docker.com/

        For more examples and ideas, visit:
         https://docs.docker.com/get-started/


#### 2.2. Check if you have downloaded the HLA-arena image:
In the command line (or prompt) run the following command:

        docker images

You should see an output like this:

        REPOSITORY             TAG                      IMAGE ID            CREATED             SIZE
        kavrakilab/hla-arena   latest                   e6cefe68c72a        2 months ago        20.6GB

#### 2.3. Modeller license key
Several of HLA-Arena workflows rely on Modeller to perform the homology modeling of a given HLA receptor. This modeling task is integrated into a specific HLA-Arena function (more details [here](https://kavrakilab.github.io/hla-arena/DOCUMENTATION.html)). However, using Modeller requires you to register and obtain your own license key, if you do not already have one. First, follow instructions on the [Modeller registration page](https://salilab.org/modeller/registration.html).

Once you have the key, you can permanently update the HLA-Arena container with your key. For that, you should execute the commands below, replacing MODELLER_KEY with the correct key.

        docker run -it kavrakilab/hla-arena
        sed -i "s/XXXX/MODELLER_KEY/g" /conda/envs/apegen/lib/modeller-9.20/modlib/modeller/config.py
        exit
        docker commit $(docker ps -a | sed -n 2p | awk '{ print $1 }') kavrakilab/hla-arena
        docker container rm $(docker ps -a | sed -n 2p | awk '{ print $1 }')

For more information on HLA-Arena, you can check the [HLA-Arena github repository](https://github.com/KavrakiLab/hla-arena).

We also have a two-part tutorial available on YouTube:

[HLA-Arena video tutorial (Part 1)](https://youtu.be/gIFHmejEulo)

[HLA-Arena video tutorial (Part 2)](https://youtu.be/fPhnmYez4QA)
