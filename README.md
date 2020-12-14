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

1.	Use LabelImg or other tools to label your data in PASCAL VOC format. Store images and annotations in Dataset/training_20201220.
2.	Create new folder: Dataset/custom/annotations
3.	Put your corre_custom.npy, list_obj.txt and list_vb.txt into Dataset/custom/annotations.  
4.  cd src
5.  Convert annotations from .xml to .json and copy images to custom
`python3 pascal2json.py --input-folder Dataset/training_20201220 --output-folder Dataset/custom`
Warning: This script only  works if there is only one Person. Objects will be annotated as No_Interaction with that Person.

## Train
`cd src`  
Modify num_classes, num_classes_verb, default_resolution  
`vim src/lib/datasets/dataset/custom.py`  
Modify default_dataset_info  
`vim src/lib/opts.py. default_dataset_info`  
Modify rules to save model: if epoch > 100:  
`vim main.py`  
`python3 main.py  custom --batch_size 12 --master_batch 7 --lr 5e-5 --gpus 1,2 --num_workers 0  --load_model ../models/ctdet_coco_dla_2x.pth --image_dir images/train --dataset custom --exp_id custom --num_epochs 200`  

## Test

## Visualization
