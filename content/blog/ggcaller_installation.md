---
title: "ggCaller installation"
description: "More information on ways to install of ggCaller"
date: 2024-04-25
featured_image: '/images/header16.jpg'
draft: false
type: "post"
author: "Raymond Cheng & Lale Maouloud"
---

{{< toc >}}

**Prerequisites**

Before you begin, make sure your system meets the following requirements:

- [x] **Operating System**: Linux (recommended) or macOS.
- [x] **Compiler**: GCC (GNU Compiler Collection) version 4.8 or higher.
- [x] **CMake**: Version 3.1.0 or later.
- [x] **Git**: Version 2.0 or later.
- [x] **Python**: Version 3.6 or later.
- [x] **Pip**: Python package installer.
- [x] **Basic familiarity** with the command line interface.

Please download the example fasta files from this [link](https://figshare.com/articles/dataset/Bentley_et_al_2006_CPS_sequences/21829038).
These fasta files will be the input of ggCaller.


## Installing ggCaller from Source

> Installing ggCaller from source ensures that you have the most up-to-date version, tailored to your specific operating system. This tutorial will guide you through the installation process, from setting up your environment to verifying the successful installation.


To install ggCaller from source, you first need to set up your environment with the required packages, which are listed in either [environment_linux.yml](https://github.com/bacpop/ggCaller/blob/master/environment_linux.yml) or [environment_macOS.yml](https://github.com/bacpop/ggCaller/blob/master/environment_macOS.yml) based on your OS. You'll also need a C++17 compiler, such as gcc version 7.3 or higher. After setting up the environment using Conda, clone the ggCaller repository and install it with Python setup tools.


### Overview

1. **Clone the ggCaller repository** with a recursive flag to include submodules.
2. **Create and activate a Conda environment** using the provided YAML file.
3. **Install ggCaller** using Python setup.

### Step-by-Step Guide

#### Step 1: Clone ggCaller Repository

1. Open a terminal window.
2. Execute the command below to clone the ggCaller repository from [GitHub](https://github.com/bacpop/ggCaller/tree/master):

```bash
git clone --recursive https://github.com/samhorsfield96/ggCaller && cd ggCaller
```

This command downloads the latest version of ggCaller to your local machine and moves you into the `ggCaller` directory.

#### Step 2: Create and Activate a Conda Environment

1. To create a new environment and install the necessary dependencies, execute:

For Linux users:

```bash
conda env create -f environment_linux.yml
```

For macOS users:

```bash
conda env create -f environment_macOS.yml
```
You will see the following messages:
![](/images/ggCaller_install/create_conda_env.png)

2. Activate the newly created Conda environment:

```bash
conda activate ggc_env
```
You will see the following messages:
![](/images/ggCaller_install/conda_activate.png)
#### Step 3: Install ggCaller

1. With the environment set up and activated, you can now install ggCaller. Run the setup script by executing:

```bash
python setup.py install
```
You will see the following messages:
![](/images/ggCaller_install/python_install.png)

#### Step 4: Verify Installation

To ensure ggCaller is correctly installed:

1. Open a new terminal window.
2. Check the installation by running:

```bash
ggcaller --version
```
You will see the following messages:
![](/images/ggCaller_install/ggcaller_version.png)

If you wish to view the ggCaller help message and confirm it's ready for use, type:

```bash
ggcaller -h
```

You should see the ggCaller help message, indicating a successful installation.

Congratulations! You've successfully installed ggCaller from source. You're now ready to use this powerful tool for your genomic analysis.


## Installing ggCaller with Docker

> Installing ggCaller with Docker avoid software dependency problem, as the docker image encapsulates applications and their dependencies needed, ensuring consistency across different environments.

### Step1: Download Docker Desktop (Mac):
1. Go to the [Docker Desktop for Mac page](https://docs.docker.com/desktop/install/mac-install/) on the Docker website. Click the **“Download from Docker Hub”** button to download the Docker Desktop installer

2. Install Docker Desktop:
Open the downloaded .dmg file to mount the Docker Desktop disk image.
Drag the Docker icon to the Applications folder.

3. Run Docker Desktop:
Open Docker Desktop from your Applications folder.

4. Configure Resources (Optional):
In the Docker Desktop preferences, you can configure resources such as CPU, memory, and disk space allocated to Docker containers. Adjust these settings based on your system resources.

5. Start Docker Desktop:
Click the Docker Desktop icon in your Applications folder to start Docker. The Docker icon in the menu bar indicates that Docker is running.

6. Verify Installation:
To verify that Docker is installed and running, open **Terminal** and run the following commands:
```
docker --version
```
You will see the following messages:
![](/images/ggCaller_install/docker_version.png)

### Step2: Download ggcaller by Docker
1. Download ggCaller docker image
```
docker pull samhorsfield96/ggcaller:latest
```
You will see the following messages:
![](/images/ggCaller_install/docker_pull.png)

2. check the image is downloaded properly, list the downloaded images
```
docker images
```
You will see the following messages:
![](/images/ggCaller_install/docker_image.png)

### Step3: Run ggcaller **Gene-calling** mode
1. Prepare input files:
Create a directory and place all the assembly files (.fasta or .fa) that you want to analyse in the directory

2. In the directory with fasta files, generate a **input.txt** file listing all the filenames of the assembly files
```
ls -d -1 *.fa > input.txt
```

3. Run ggCaller gene-calling
```
docker run --rm -it -v $(pwd):/workdir samhorsfield96/ggcaller:latest ggcaller --refs input.txt
```

without specifying the output directory name, you will expect to see a new directory called **_```ggCaller_output```_** storing the output files:
![](/images/ggCaller_install/genecall_output.png)

Congratulations! You've successfully installed ggCaller with Docker. You're now ready to use this powerful tool for your genomic analysis.



## More information about ggCaller
For more information about ggCaller, please refer to ggCaller documentation [here](https://ggcaller.readthedocs.io/en/latest/index.html).
You can also find a nice and succinct introduction of ggCaller [here](https://www.bacpop.org/blog/ggcaller/).





