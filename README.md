# Agricultural Satellite Image Classifier 

## Introduction

This github repo has been created to store files related to the Agricultural Vision Segmentation Challenge. The dataset contains 21,061 aerial images of farmland in the United States. Each image contains 512x512 color channels which are RGB and Near Infra-Red. The images come with bounded copies indicated region of the farmland. The mask indicates valid pixels. 

Pattern recognition from aerial agricultural images presents several challenges. This includes the variations of patterns you are looking to classify, the amount of annotated patters and the properties of the annotation(like shape, texture or depth). This distinguishes aerial pattern recognition from object recognition and the former is a more challenged task. To quote the creators of the dataset "semantic segmentation of aerial farmland images requires inference over extremely large-size images with extreme annotation sparsity. These challenges are not present in most of the common object datasets, and we show that they are more challenging than many other aerial image datasets.

## Business Value 

With the growth of global populations, agriculture is being placed under increasing pressure to increaze yields and maximize efficeny. Satellite images have become regularly employed to monitor agricultural activities and provide important data to estimate crop conditions and yields. 

This project seeks to develop a set of best practices that can be applied to current and historical satellite data to identify and segment images based on several important features that impact crop yield. The classifier developed in this project can be deployed by farmers and agricultural researchers to identify critical features in their field and better understand the impacts these can have on yield. I hope that by building this project, data science can be used to improve security for people worldwide and that farmers are secure in knowing that they have access to the best technology, research and data possible. 

## Process/Methodology

Model Evaluation:
This notebook contains the most successful models based on the previous 2 weeks of testing and optimization. A peak classification rate of 76% was achieved based on optimizing and improving previous models. Adjustments to the loss function and out put layer were made. 

Both resnet and vgg16 were experiments with but proved ineffective at categorizing the imbalanced dataset both with and without augmnentation. The gradients exploded or went to zero and the multiple changes of batch size and loss function were unsuccesful.

The CNN classifier used proved to be most effective with a starting accuracy of 70% that was increased by using an adam optimizer and 20 epochs. The results can be seen below.

<b> Results </b>

| Model       | Accuracy    |
| ----------- | ----------- |
| 72_88_bin_seq | 71%       |
| adam_78  | 76%         |
| rmsprop     | 73%            |
| test model     | 64%            |


<b> Classification Report </b>

![image](images/classification_report.png)


## Example Prediction
![image](images/double_planter.png)

<b> Predictions </b> 

| Category   | Probability  |
| ----------- | ----------- |
| double_planter | 0.824       |
| weed_cluster  | 0.0443         |
| standing_water     | 0.0193     |


## Analysis and Improvements
In order to further improve the model, many more experiments would need to be carried out to optimize the epochs, batch size, loss function and layers.

The best model was trained on 20 epochs and this enabled the cnn to pick up the features that distinguish weed clusters from everything else. Distinguishing weed clusters and cloud shadows is very important to other targets as weed clusters can be confused for grass around waterways. Cloud shadows are also veyr important in satellite imaging and impacts the ability to recognize other characteristics.

Future models could be improved by removing planter skips and training these in a seperate model to understand how to get these picked up. Further work on pixel segmentation would be also improve performance as single images can contain multiple target variables which can decrease accuracy of classifcation.


##  Target variables  & Their Relevance to Agriculture:

There are 6 target variables: Cloud shadow, Double plant, Planter skip, Standing Water, Waterway and Weed cluster. These features are considered to have large impacts on the yield of farmland. Improving the ability to locate them is relevant to improving potential yields on farmland. There is a high level of difficulty in adressing potential overlaps between patterns and finding the best ways to process such a large amount of data in a memory efficent way.

### Cloud_Shadow: 
Cloud coverage is common at critical times of the agricultural season. This cloud coverage impacts the ability of remote sensing technologies such as satellites from obtaining clear views of the earth. Understanding and classifying these will improve the ability to create clearer images in the future. 

### Double Planter: 
Double planting means planting multiple crops in the same area and in same yeaer so that theland can be used to genreate more than one crop per year. Identifying this is critical to evaluating the health of a field, managing water resources and improving soil quality. 

### Planter_Skip: 
A planter is farm implement that sows eeds in rows through a field. Effective use of this tool remotely requires equipping it with locational awareness. Efficent use of planters is critical. By understanding the patterns left behind by planters, the optimum time, soil quality and environmental factors can be deduced. 

### Standing_Water: 
Most crops cannot survive for long under water. Waterlogged fields can cause problems for crop yields and pose long term threats to the environment. By identifying the location of these, not only can crops be saved but drainage sysems can be planned around it.

### Waterway:
Waterways are critical in both providing water for agriculture via irrigation and for the health of the surronding populations that may rely on the waterway as a key source of drinking water. Identifying waterways can enable better irrigation planning and environmental resource management to ensure industral waste is not running off into the river. 

### Weed Cluster: 
Weed clusters have significant impact on the productivity of crop yields and identifying them is critical to preventing their growth. Due to the prevalence of this in fields, it represent a big part of our dataset.

The target variables are plotted below:

![image](images/target_variables.png)

## Files in Repo

### Helper Functions 

<b> Single Image Classifier</b>
Can take in an image and display a predicted class along with the image. Works fine for train data but it sees weed clusters everywhere for the test data. Model used is 85% at .65 loss function. Uses an uploaded h5 file. 

<b> Export_files_to_google_bucket: </b>
Created a google bucket to store files from google drive in the google cloud platform. The goal of this is to be a cloud based database that can handle high volums of requests. It also enables easier analysis regardless of local computing power. 

<b> Sorting RGB Files: </b>
This file contains helper functions to sort images in unlabelled folders(such as rgb/nir) into their respective categories. This can be used to create better training data.

### Models

<b> Adam Optimizer - 73% </b>
First attempt at a model with decent accuracy. Improved in the next notebook.

<b> Adam Optimizer 20 epochs </b>
Added more epochs. Changed batch size but found 32 worked best. 

<b> Create_train_set_fit_model: </b>
Create a trained model 2000 images. The random state in train_test_split really impacted the loss function and precision. This is a messy file with a bit of everything but leaving as is, as it works. The model can be loaded like in the Quick Classifier. 

<b> CNN_1: </b>
A low layer model that produced exploding gradients. Useful for testing but not a good model. 

<b> Create_train_set_fit_model: </b>
Create a trained model 2000 images. The random state in train_test_split really impacted the loss function and precision. This is a messy file with a bit of everything but leaving as is, as it works. The model can be loaded like in the Quick Classifier. 

<b> Model_Evaluation</b>

This contains all the working models, information on their parameters, visualisations of the layers and their performance. Useful to see what worked best and why.



Sources:
Agriculture-Vision: A Large Aerial Image Database for Agricultural Pattern Analysis
https://arxiv.org/abs/2001.01306
