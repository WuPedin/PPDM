# PPDM
Apply PPDM on customized datasets

This repository is modified from https://github.com/YueLiao/PPDM.  
To train on HICO-Det and HOI-A datasets, please check https://github.com/YueLiao/PPDM.  

To train and inference on customized datasets, please follow the steps below:

## Environment
    sudo docker build -t hoi/ppdm .  
    sudo docker run --runtime=nvidia --name ppdm --shm-size 8G -t -i hoi/ppdm:latest /bin/bash  
    git clone https://github.com/WuPedin/PPDM.git

## Generate Customized Dataset
Warning: This script only  works if there is only one Person. Objects will be annotated as No_Interaction with that Person.
1.	Use LabelImg or other tools to label your data in PASCAL VOC format.
2.	Create new folder: custom/annotations
3.	Put your corre_custom.npy, list_obj.txt and list_vb.txt into custom/annotations.
    Generate corre.npy like this:
    Objects: Person, Bed
    Verbs: Sit, Lie, Stand
    da = np.array([[0,1],
               [0,1],
               [0,1]], dtype=np.float16)
    np.save('corre_custom.npy', da)              

## Train

## Test

## Visualization
