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

<!-- <img src="https://user-images.githubusercontent.com/85773711/135238981-b7e6b363-32ed-4152-8434-fb03d1f5d530.png" width="300" align="center"/> -->
```
Layer (type)                 Output Shape              Param #   
=================================================================
conv2d_6 (Conv2D)            (None, 214, 214, 32)      11648     
_________________________________________________________________
max_pooling2d_6 (MaxPooling2 (None, 106, 106, 32)      0         
_________________________________________________________________
conv2d_7 (Conv2D)            (None, 102, 102, 64)      51264     
_________________________________________________________________
max_pooling2d_7 (MaxPooling2 (None, 50, 50, 64)        0         
_________________________________________________________________
conv2d_8 (Conv2D)            (None, 46, 46, 128)       204928    
_________________________________________________________________
max_pooling2d_8 (MaxPooling2 (None, 22, 22, 128)       0         
_________________________________________________________________
flatten_2 (Flatten)          (None, 61952)             0         
_________________________________________________________________
dense_4 (Dense)              (None, 1024)              63439872  
_________________________________________________________________
dense_5 (Dense)              (None, 300)               307500    
=================================================================
Total params: 64,015,212
Trainable params: 64,015,212
Non-trainable params: 0
_________________________________________________________________
```

In this approach, base model have ... accuracy and ... f1 score on test set
### MobienetV2
I use pretrain mobienetv2 on imagenet competion with 1000 classes
#### Freezing all mobienetv2 layers, only train on last classifier layer


<!-- <img src="https://user-images.githubusercontent.com/85773711/135242463-0161722c-48f7-4ba3-9c92-e68c9980bd2c.png" width="300" align="center"/> -->
```
Layer (type)                 Output Shape              Param #   
=================================================================
input_8 (InputLayer)         [(None, 224, 224, 3)]     0         
_________________________________________________________________
sequential_1 (Sequential)    (None, 224, 224, 3)       0         
_________________________________________________________________
tf.math.truediv_3 (TFOpLambd (None, 224, 224, 3)       0         
_________________________________________________________________
tf.math.subtract_3 (TFOpLamb (None, 224, 224, 3)       0         
_________________________________________________________________
mobilenetv2_1.00_224 (Functi (None, 7, 7, 1280)        2257984   
_________________________________________________________________
global_average_pooling2d (Gl (None, 1280)              0         
_________________________________________________________________
dropout_1 (Dropout)          (None, 1280)              0         
_________________________________________________________________
dense_3 (Dense)              (None, 300)               384300    
=================================================================
Total params: 2,642,284
Trainable params: 384,300
Non-trainable params: 2,257,984
```
<img src="https://user-images.githubusercontent.com/85773711/135242855-6ccbb98d-ab3f-4ca0-9696-6ae9c34b2629.png" width="450" align="center"/>

#### Fune tuning on mobienetv2
In this approach, I unfreeze some top layers and fine tune model 

<!-- <img src="https://user-images.githubusercontent.com/85773711/135243776-6ca29053-9a45-4eaa-9a8e-46e9e0b4aedc.png" width="300" align="center"/> -->
```
Layer (type)                 Output Shape              Param #   
=================================================================
input_8 (InputLayer)         [(None, 224, 224, 3)]     0         
_________________________________________________________________
sequential_1 (Sequential)    (None, 224, 224, 3)       0         
_________________________________________________________________
tf.math.truediv_3 (TFOpLambd (None, 224, 224, 3)       0         
_________________________________________________________________
tf.math.subtract_3 (TFOpLamb (None, 224, 224, 3)       0         
_________________________________________________________________
mobilenetv2_1.00_224 (Functi (None, 7, 7, 1280)        2257984   
_________________________________________________________________
global_average_pooling2d (Gl (None, 1280)              0         
_________________________________________________________________
dropout_1 (Dropout)          (None, 1280)              0         
_________________________________________________________________
dense_3 (Dense)              (None, 300)               384300    
=================================================================
Total params: 2,642,284
Trainable params: 2,245,740
Non-trainable params: 396,544
```
<img src="https://user-images.githubusercontent.com/85773711/135243826-a23e05fe-7d01-46c1-ae94-48dbc2a5b184.png" width="450" align="center"/>

After fine tunning, model have  ... accuracy and ... f1 score on test set
