# Bird classification
## Task Description
- Task: Birds Classification.
- Dataset: 
  + Training set: 43622 images belonging to 300 classes.
  + Validation set: 1500 images belonging to 300 classes.
  + Test set: 1500 images belonging to 300 classes.
  + You can download dataset here: https://www.kaggle.com/gpiosenka/100-bird-species/code

<img src="https://user-images.githubusercontent.com/85773711/135237477-04f35a76-3f97-4acf-a1d8-8cb297ca9039.png"  align="center"/>

## Implement
### Base model
I implement a simple CNN model

<img src="https://user-images.githubusercontent.com/85773711/135238981-b7e6b363-32ed-4152-8434-fb03d1f5d530.png" width="300" align="center"/>

In this approach, base model have ... accuracy and ... f1 score on test set
### MobienetV2
I use pretrain mobienetv2 on imagenet competion with 1000 classes
#### Freezing all mobienetv2 layers, only train on last classifier layer


<img src="https://user-images.githubusercontent.com/85773711/135242463-0161722c-48f7-4ba3-9c92-e68c9980bd2c.png" width="300" align="center"/>
<img src="https://user-images.githubusercontent.com/85773711/135242855-6ccbb98d-ab3f-4ca0-9696-6ae9c34b2629.png" width="300" align="center"/>

#### Fune tuning on mobienetv2
In this approach, I unfreeze some top layers and fine tune model 

<img src="https://user-images.githubusercontent.com/85773711/135243776-6ca29053-9a45-4eaa-9a8e-46e9e0b4aedc.png" width="300" align="center"/>
<img src="https://user-images.githubusercontent.com/85773711/135243826-a23e05fe-7d01-46c1-ae94-48dbc2a5b184.png" width="300" align="center"/>

After fine tunning, model have  ... accuracy and ... f1 score on test set
