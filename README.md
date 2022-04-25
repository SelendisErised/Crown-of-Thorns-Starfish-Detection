# COTS Detection on the Great Barrier Reef
## Project Overview
The world’s largest coral reef, the Great Barrier Reef is home to around 400 species of corals. The reef is now under threat because of the overpopulation of a specific species of starfish called crown-of-thorns starfish(COTS), which are destroying many of the native corals.

Our task is to identify locations (bounding box) of COTS from underwater images of the Great Barrier Reef, aiming to improve the efficiency and scale at which reef managers detect and control COTS outbreaks. This will help measures being taken to bring down the levels of COTS to a more ecologically sustainable level.

You could find the dataset we used at https://www.kaggle.com/competitions/tensorflow-great-barrier-reef/data.

![](Image/COTS.png)

## Main Scripts

1. [COTS_download.ipynb](Code/COTS_download.ipynb)

  Help to download the *Help Protect the Great Barrier Reef* dataset using Kaggle API to your own google drive under  `/content/drive/MyDrive/Protect_Reef`.

2. [COTS_cleaning_and_sampling_merged.ipynb](Code/COTS_cleaning_and_sampling_merged.ipynb)

  Help to visulize and analyze the basic informations about experimented data. Perform data cleaning and sampling. Prepare the training and validation data. Change the label to YOLO format. The images and labels are stored under  `/content/drive/MyDrive/Protect_Reef_Process`.

3. [COTS_yolov5s6_train.ipynb](Code/COTS_yolov5s6_train.ipynb)

  Use yolov5s6 to train the model and report the validation results. This file includes all the megadata and augmentations configuration. The training process for 15 epochs will last for about 7.5 hr. The trained model will be stored under `/content/drive/MyDrive/Protect_Reef_Process/yolov5s6`.

4. [COTS_yolov5n6_train.ipynb](Code/COTS_yolov5n6_train.ipynb)

  Use yolov5n6 to train the model and report the validation results. This file includes all the megadata and augmentations configuration. The training process will last for about 7.72 hr. The trained model will be stored under `/content/drive/MyDrive/Protect_Reef_Process/yolov5n6`.
 
5. [COTS_yolov5_validation.ipynb](Code/COTS_yolov5_validation.ipynb)

  Help to output the validation results for the former training process. The validation result should be shown after training normally. Just in case we met some errors like exceeded GPU memory. This notebook could also be used to check the validation result for the ensembling models.

6. [yolov5-s6-n6-ensemble.ipynb](Code/yolov5-s6-n6-ensemble.ipynb)

  Use Weighted Box Fusion (WBF) to ensemble the trained yolov5s6 and yolov5n6 model. Evaluate the performace of the ensembling model on the hidden test set through Kaggle API.

**Note: This project is mainly trained on Google Colab. Run the script 1-5 in the above order to retrain the model. Model ensembling and model evaluation (script 5) was finished in Kaggle Notebook environment. Please put the trained models to the corresponding paths to reproduce the results.**

## Trained models & Metrics

The trained model and result are stored under /Model, including all the output file. The model is in pytorch format, i.e., model_name.pt. All the models are trained on a resolution of 1280 x 720 and only using images with boxes. For augmentations, we employ a mix of flips, scales, HSV, mosaic, etc. For validation, we use group k fold (k=3), that is to say, the same group will not appear in two different folds. The overall architecture is designed based on [YOLOv5](https://github.com/ultralytics/yolov5). We trained yolov5s6 and yolov5n6 for different epochs. Due to the runtime limitations of colab, we cannot trained more complex models like yolov5l6, which may have better performance. In this case, we use ensemble methods to optimize our model. 

## Ensemble

We use ensemble methods to upgrade our model performances. As long as the base models are diverse and independent, the prediction error decreases when the ensemble approach is used. Here, we use a state of art method for combining predictions of object detection models: [Weighted Box Fusion (WBF)](https://arxiv.org/abs/1910.13302). Unlike NMS and soft-NMS methods that simply remove part of the predictions, the weighted box fusion (WBF) method, introduced by Roman Solovyev et al. in 2019, uses confidence scores of all proposed bounding boxes to construct the average boxes.

## Test Result (Competition Submission Score)

| Model      | Private Score | Public Score  |
|    :-----:    |    :----:   |    :---: |
| yolov5n6      | 0.310       | 0.348   |
| yolov5s6   | 0.330        | 0.457      |
| WBF (n6 & s6)   | 0.424        | 0.358      |

## Reference

1. Kaggle: TensorFlow - Help Protect the Great Barrier Reef,  https://www.kaggle.com/competitions/tensorflow-great-barrier-reef.
2. Ultralytics, YOLOv5 🚀 in PyTorch, https://github.com/ultralytics/yolov5
3. Solovyev, Roman, Weimin Wang, and Tatiana Gabruseva. "Weighted boxes fusion: Ensembling boxes from different object detection models." Image and Vision Computing 107 (2021): 104117. https://arxiv.org/abs/1910.13302
4. Weighted Box Fusion, https://github.com/ZFTurbo/Weighted-Boxes-Fusion
5. BBOX Helper, https://github.com/awsaf49/bbox
