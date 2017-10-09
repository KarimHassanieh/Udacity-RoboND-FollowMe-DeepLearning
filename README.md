## Project Details

## Objective & Goal :

The purpose of this excercise is to preform  object-human tracking by developing a deep learning network that locates a particular human target within an image. This deep learning model  will allow a simulated quadcopter to follow around the person that it detects!

## Additional Submissions :
In addition to this report note that the html version of the notebook  and .h5 files of the weights (in weights forlder) are submitted as part of this repository.

## 1- Network Architecture : 

__Nueral Network  Architecture & Philosophy :__

The network architecture used is that of a fully convolutional network. Such networks are widely used for object tracking in computer vision application and robotics. The reason an architecture of fully convolutional network is chosen over previously used fully connected layer is because spatial information of where the object recognized in the image is preserved which is needed when tracking objects.

The fully convolutional nueral network is composed of 3 main stages, the encoding stage, the implementation of 1x1 convlutional layer, and the decoding stage. In the below table is a summary of the network architecture developed for our application. This architecture has been found to be opitimal for our application after many experimentation. 

| Layer Number       | Purpose       | Layer Size and Dimension          | Layer Depth  |
| ------------- | ------------- |:-------------:| -----:|
| Layer 1        | Input Layer-Image | 160 x 160 | 3 |
| Layer 2       | Encoder 1 | 80 x 80 | 64 |
| Layer 3       | Encoder 2 | 40 x 40 | 128|
| Layer 4       | 1 x 1 layer | 20 x 20 | 256 |
| Layer 5       | Decoder 1 | 40 x 40 | 128|
| Layer 6       | Decoder 2 | 80 x 80 | 64 |
| Layer 7       |Output Layer | 160 x 160 | 3 |


<p align="center"><img src="./Images/archi.jpg" /></p>

__Encoding Layers :__

An encoding layer is implemented to extract the features and distictinve features in the image. In principal encoding layers can be used mainly for object recognition in an image. In our implementation 2 encoding layer have been used. The first layer takes an image of 3 layers (R-G-B) and ouputs a layer of depth 64 (layer 2). The second layer we implement a filter size of 128 and decreasing its size by half as well (layer 3).

In terms of image manipulation downsampling an image will help extract the simple patterns in the input image and gradually learn the complex structure and shapes in deeper layers.

__1x1 Convolutions :__

The 1x1 convolution is used to change the dimensionality in filter space (in our case at layer 4  from 128 to 256) while preserving the distinctive feature and charactecterstics of the previous encoded layer.


__Decoding Layers :__

Decoding layers are implemented at the end of the neural network model to retreive spatial infromation, in our case to locate the recognized object's location in the image, such necessary infromation may have been lost due to the encoding and downsizing of the image. During decoding stage bileniar upsampling by 2 is preformed through 2 different decoding layers. 
 The first decoding layer is then convoluted with a filter of depth 128 (layer 5) while the second decoding layer is then convoluted again with a filter of depth 64 (layer 6). In such method the layer depth decreases from one layer to another. Also in each decoding the image is upsampled by a factor of 2 to retreive the spatial information.

The bilinear upsampling method in terms of image manipulation allows for the recovery of the image in its initial sizing dimension pixel wise and allows for the recovery of spatail information needed to indetify location of the object in the image.


__Skip Connections :__

 Skip connections are implemented among non-adjacent layers to maintain information which could have been lost as result of the encoding stage. In our case there are 3 connections.
 The first connection is between the first and last layers. 
 The second connection is between Layer 2 with layer 6. 
 Finally a third connection exists between Layer 3 and Layer 5.

__Hyper Parameters :__

The needed hyper parameters were tuned by experimentation. Initially the learning rate was at 0.01 however despite the fact that the training process was faster however the accuracy scoring was lower then 40%. Thurefore the learning rate  was decreased to 0.005 at the cost of the computing speed for the training process. Also it was noted that based on the learning rate of 0.005 increasing the number of epochs helped increase the accuracy of the model. Thurefore  the number of epochs was experminted and found to be optimal at 100 (initailly 5).

No of Parameters | Learning Rate | Batch Size | Number of Epochs | Steps Per Epoch  | Validation Steps | Workers
--- | --- | --- | --- | ---| --- | ---
6 | 0.005 | 32 | 100 | 200| 50| 4





## 2- Training and Results : 

__Setup :__

The nueral network was initailly trained on a processor of Intel® Core™ i7-7500U CPU @ 2.70GHz × 4.  For 5 epochs on the local computer (Training time took 3 hours) and initially acheived a result of 36% accuracy. However it was evident that the number of epochs had to increase to improve the accuracy of the model. In order to speed up the training process AWS instances (p2.xlarge instance) were used and for 100 epochs. Training with AWS for 100 epochs took around 4 hours to complete.  

__Results :__

The final accuracy result received based on the above mentioned hyperparameters was __41.8%__ which is above the required passing score of 40%. However this result can be further improved. 

The below image shows the output of the training process. The model was trained for 100 epochs using AWS instances. 
<p align="center"><img src="./Images/result.png" /></p>

## 3- Conclusions & Future Work : 

While the result obtained is above what is required it can still be enhanced. More data can be collected to improve the accuracy of the nueral network. In addition more experimentation can be done on the hyper paremeters to obtain better results.

Also the network can be further enhanced to track other then humans but also dogs, cats and other animals. However in order to do this more data has to be collected and obtained in order for the neural network to identify such objects. Once data is collected the network has to be trained in order to accurately identify the new type of objects.
