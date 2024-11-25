#  Install MLFlow with UI 
## Requirement 
* Anaconda ENV **OR** 
* Miniconda ENV **OR**
* Python ENV  
* Ubuntu 22.04
### I Use Miniconda for install MLFlow on Ubuntu 22.04

## Quick command line install
#
    sudo apt update 
# 
    mkdir -p ~/miniconda3
# 
    wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda3/miniconda.sh
# 
    bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3
# 
    rm -rf ~/miniconda3/miniconda.sh

#### suppose conda base not open or conda command not work use below command 
# 
    bash 

## Create conda environment 
#
    conda create -n dvc python=3.11 -y 
# 
    conda activate mlflow 
### Install MLFlow using conda command 
#
    conda install -c conda-forge mamba -y
# 
    mamba install -c conda-forge dvc -y 
#### for verify us below command 
#
    dvc --version 
# Thank You 