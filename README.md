# Agricultural Satellite Image Classifier 

## Introduction

This github repo has been created to store files related to the Agricultural Vision Segmentation Challenge. The dataset contains 21,061 aerial images of farmland in the United States. Each image contains 512x512 color channels which are RGB and Near Infra-Red. The images come with bounded copies indicated region of the farmland. The mask indicates valid pixels. 

There are 6 target variables: Cloud shadow, Double plant, Planter skip, Standing Water, Waterway and Weed cluster. These features are considered to have large impacts on the yield of farmland. Improving the ability to locate them is relevant to improving potential yields on farmland. There is a high level of difficulty in adressing potential overlaps between patterns and finding the best ways to process such a large amount of data in a memory efficent way.

The target variables are plotted below:

![image](target_variables.png)

##  Target variables  & Their Relevance to Agriculture:

### Cloud_Shadow: 
Cloud coverage is common at critical times of the agricultural season. This cloud coverage impacts the ability of remote sensing technologies such as satellites from obtaining clear views of the earth. Understanding and classifying these will improve the ability to create clearer images in the future. 

### Standing_Water: 
Most crops cannot survive for long under water. Waterlogged fields can cause problems for crop yields and pose long term threats to the environment. By identifying the location of these, not only can crops be saved but drainage sysems can be planned around it.

### Planter_Skip: 
A planter is farm implement that sows eeds in rows through a field. Effective use of this tool remotely requires equipping it with locational awareness. Efficent use of planters is critical. By understanding the patterns left behind by planters, the optimum time, soil quality and environmental factors can be deduced. 


## Current Progress

<b> Quick Classifier: </b>
Can take in an image and display a predicted class along with the image. Works fine for train data but it sees weed clusters everywhere for the test data. Model used is 85% at .65 loss function. 

Uses an uploaded h5 file. 


<b> Create_train_set_fit_model: </b>
Create a trained model 2000 images. The random state in train_test_split really impacted the loss function and precision. This is a messy file with a bit of everything but leaving as is, as it works. The model can be loaded like in the Quick Classifier. 

