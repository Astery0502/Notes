# The config and pipeline for Jupyter installation on Remote Linux server #

## Pre Environment Build ##

### Server security and preparation ###

> to be set with local port forwarding

### Vim ###

copy the repository on Github and mv the .vimrc --> to be set

### Miniconda ###

1. get the install bash and start installation.

```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh
```

2. create a environment (python3.8 for idlpython bridge requirement):

```conda
conda create -n idlpython python=3.8
```

3. install required packages through pip:

First check the pip:
```
sudo apt upgrade pip
```

Or if not installed:
```
sudo apt install python3-pip
```

Install the jupyterlab 
```
pip install jupyterlab
```

### Jupyterlab config ###

From [Jupyterlab homepage](https://jupyter-notebook.readthedocs.io/en/stable/public_server.html)

#### Securing a notebook server

Set a password manully: configure the *NotebookApp.password* setting in **jupyter_notebook_config.py**.

1. Prerequisite: A notebook configuration file

```
jupyter notebook --generate-config
```

2. Automatic password setup (including hassed password setup)

see [jupyterlab password setup](https://jupyter-notebook.readthedocs.io/en/stable/public_server.html#automatic-password-setup)

3. set the remote access *True*

4. SSL for encrypted communication

5. 

### Enter the remote Jupyterlab ###

enter **RemoteIP:port/lab**

## Error ##
1. unhandled error about kernel: caused from *conda pack* the kernel file points to the python of the temp dir (as compressed file)  
use **conda speckernel list** to show the location and change the pointer to the right location
