## Project Details

## Objective & Goal :

The purpose of this excercise is to preform  semantic segmentation by developing a deep learning network that locates a particular human target within an image.This deep learning model that will allow a simulated quadcopter to follow around the person that it detects!

## Additional Submissions :
In addition to this report note that the html version of the notebook  and .h5 files of the weights (in weights forlder) are submitted as part of this repository.

## 1- Network Architecture : 

| layers        | dimension           | depth  |
| ------------- |:-------------:| -----:|
| input layer | 160 * 160 | 3 |
| encoder 1 | 80 * 80 | 128 |
| encoder 2 | 40 * 40 | 64 |
| encoder 3 | 20 * 20 | 32 |
| 1 x 1 layer | 20 * 20 | 32 |
| decoder 1 | 40 * 40 | 32 |
| decoder 2 | 80 * 80 | 64 |
| decoder 3 | 160 * 160 | 128 |

__Network Layers & Architecture :__

The network architecture used is that of a fully conv




__Encoding Layers :__

An encoding layer is implemented to extract the features in the image 

__1x1 Convultions :__

__Fully Connected Layers :__

__Decoding Layers :__

__Hyper Parameters :__

No of Parameters | Learning Rate | Batch Size | Number of Epochs | Steps Per Epoch  | Validation Steps | Workers
--- | --- | --- | --- | ---| --- | ---
6 | 0.005 | 32 | 100 | 200| 50| 4





## 2- Training and Results : 

__Setup :__
The nueral network was initailly trained for 5 epochs on the local computer (Training time took 3 hours) and initially acheived a result of 36% accuracy. However it was evident that the number of epochs had to increase to improve the accuracy of the model. In order to speed up the training process AWS instances (p2.xlarge instance) were used and for 100 epochs. Training with AWS for 100 epochs took around 4 hours to complete.  

__Results :__

The final accuracy result received based on the above mentioned hyperparameters was __41.8%__ which is above the required passing score of 40%. However this result can be further improved. 

The below image shows the output of the training process. The model was trained for 100 epochs using AWS instances. T
<p align="center"><img src="./Images/result.png" /></p>

## 3- Conclusions & Future Work : 

While the result obtained is above what is required it can still be enhanced. More data can be collected to 

