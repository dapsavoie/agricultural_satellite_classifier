# Agricultural Satellite Image Classifier 

## Introduction

This github repo has been created to store files related to the Agricultural Vision Segmentation Challenge. The dataset contains 21,061 aerial images of farmland in the United States. Each image contains 512x512 color channels which are RGB and Near Infra-Red. The images come with bounded copies indicated region of the farmland. The mask indicates valid pixels. 

There are 6 target variables: Cloud shadow, Double plant, Planter skip, Standing Water, Waterway and Weed cluster. These features are considered to have large impacts on the yield of farmland. Improving the ability to locate them is relevant to improving potential yields on farmland. There is a high level of difficulty in adressing potential overlaps between patterns and finding the best ways to process such a large amount of data in a memory efficent way.

The target variables are plotted below:

![image](target_variables.png)


## Current Progress

<b> Quick Classifier: </b>
Can take in an image and display a predicted class along with the image. Works fine for train data but it sees weed clusters everywhere for the test data. Model used is 85% at .65 loss function. 

Uses an uploaded h5 file. 


Create_train_set_fit_model:
Create a trained model 2000 images. The random state in train_test_split really impacted the loss function and precision. This is a messy file with a bit of everything but leaving as is, as it works. The model can be loaded like in the Quick Classifier. 

