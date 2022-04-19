# COTS Detection on the Great Barrier Reef
## Project Overview
The world’s largest coral reef, the Great Barrier Reef is home to around 400 species of corals. The reef is now under threat because of the overpopulation of a specific species of starfish called crown-of-thorns (COTS), which are destroying many of the native corals.

Our task is to identify locations (bounding box) of COTS from underwater images of the Great Barrier Reef, aiming to improve the efficiency and scale at which reef managers detect and control COTS outbreaks. This will help measures being taken to bring down the levels of COTS to a more ecologically sustainable level.

You could find the dataset we used at https://www.kaggle.com/competitions/tensorflow-great-barrier-reef/data.

![](image/COTS.png)

## Main Scripts
**Note: This project is mainly finished on Google Colab. Run the notebook in the following order to reproduce the result.**

1. Code/COTS_download.ipynb

  Help to download the *Help Protect the Great Barrier Reef* dataset using Kaggle API to your own google drive under  /content/drive/MyDrive/Protect_Reef.

2. Code/COTS_previsulization.ipynb

  Help to visulize the basic information about experimented data. Prepare the training and validation data. Change the label to YOLO format. The images and labels are stored under  /content/drive/MyDrive/Protect_Reef_Process.

3. Code/COTS_yolov5s6_train.ipynb

  Use yolov5s6 to train the model and report the validation results. This file includes all the megadata and augmentations configuration. The training process for 15 epochs will last for about 7.5 hr. The trained model will be stored under /content/drive/MyDrive/Protect_Reef_Process/yolov5s6.

4. Code/COTS_yolov5m6_train.ipynb

  Use yolov5s6 to train the model and report the validation results. This file includes all the megadata and augmentations configuration. The training process will last for about ??? hr. The trained model will be stored under /content/drive/MyDrive/Protect_Reef_Process/yolov5m6.

## Trained model & Results
The trained model and result are stored under /Model, including all the output file. The model is in yolo format, i.e., model_name.pt.

## Ensemble
We use ensemble methods to upgrade our model performances.
