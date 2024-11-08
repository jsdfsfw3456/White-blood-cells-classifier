# white blood cells classification model architecture 

White blood cell (WBC) classification is a crucial task in medical diagnosis, as it helps in identifying various types of WBCs and their abnormalities. In this research work, we propose a novel deep learning-based approach for WBC classification using a customized convolutional neural network (CNN) architecture.




## Over view of Model 

![image alt](https://github.com/jsdfsfw3456/White-blood-cells-classifier/blob/bbea0073ec1645ac9a02eb5c30f0b9faba0bba62/main%20model%20architecture.png)


model is composed of four major components:

#1.Base Model(back bone) - MobilNet

#2.SK block - customized block 

#3.multifusion block - customized 

#4 Channel Attention Block (CAB) - customized 


    



## base model The model uses MobileNetV2 as the backbone architecture with pre-trained ImageNet weights
Input image size: 112x112x3
Three feature maps are extracted from different layers of MobileNetV2:

Feature1: from 'block_3_expand'

Feature2: from 'block_6_expand'

Feature3: from 'block_13_expand'

which are used to extract  features from the image. 



## SK block
This block implements selective kernel attention mechanism:

## model design of block 

![image alt](https://github.com/jsdfsfw3456/White-blood-cells-classifier/blob/f189d97e7fb90d2df86f618dd28964b19367ac6c/Sk%20block%20architecture.png)

Contains two parallel branches:

Branch1: Uses 3×3 convolutions for local feature extraction

Branch2: Uses dilated 5×5 convolutions (dilation rates 3 and 5) for larger receptive field

Features dynamic selection between different kernel sizes
Helps in capturing multi-scale information
Uses attention mechanism to adaptively adjust the importance of different receptive fields

 


## Context Attention Block 
This block enhances feature representation by:


## model design of block 

![image alt](https://github.com/jsdfsfw3456/White-blood-cells-classifier/blob/e017b2556b7a9a5b81342d31b5aaa4c248a30cb3/CAB%20block%20architecture.png)

Using depthwise convolutions with different kernel sizes (5×5 and 7×7)

Implementing channel attention mechanism
Incorporating skip connections for better gradient flow
Using GELU activation for non-linearity.

Purpose: Captures contextual information and enhances important features while suppressing irrelevant ones

## model design of block 


## Model pipeline 
1.Feature Extraction


Extracts features from three different levels of MobileNetV2
Applies spatial scaling (MaxPooling2D/UpSampling2D) to align feature dimensions


2.Feature Enhancement

Each feature map passes through the CAB Block
Features are processed through SK Block for multi-scale feature extraction
Outputs are combined  using concatenated operation


3.Classification Head

-Global average pooling

-Dense layer with 256 units and ReLU activation

-Final dense layer with 5 units (number of classes) and softmax  activation

Training Details:

Uses data augmentation (rotation, zoom, flips)

Adam optimizer

Categorical crossentropy losses
Batch size: 8, 16 ,32 
Model checkpointing for best validation accuracy



This architecture is designed to effectively capture both fine-grained details and global context necessary for accurate white blood cell classification.

## Results 



## validation accuracy 

 Trained model on PBC datasets which contain five thousands     images along with different batch sizes -8,16,32 . 
 we had got excellent results on 8 and with the training epoch -56 .

 i have got excellent results  the validation accuracy approx to 99%. which is  highest among all existing research work . 

![image alt](https://github.com/jsdfsfw3456/White-blood-cells-classifier/blob/ce186216295b7d9a7ba5f5dd9c36f2e5ceea26de/pbc%20datasets%20with%20the%203%20block%20attach%20with%20dkcab%20block%20.png)



 ## ROC curve :

 i have plot  the ROC curve for our above results 

 ![image alt](https://github.com/jsdfsfw3456/White-blood-cells-classifier/blob/5181fad8f760c9db5c8025a554a519ba24826303/ROC%20curve%20%20%20for%20it.png)




 ## confusion matrix :
 i have plot the matrix for  my results 


![image alt](https://github.com/jsdfsfw3456/White-blood-cells-classifier/blob/18b15e576289d52517857b1aab1d74e1ea73d48b/confusion%20matrix%20of%20%20white%20blood%20classification%20model.png)

 ## Training validation  accuracy plot :
  we have found very good results for it . 

![image alt](https://github.com/jsdfsfw3456/White-blood-cells-classifier/blob/7baefe6e54249dadaf527f24aff972bbb653642d/Training%20and%20validation%20accuracy%20%20for%20White%20blood%20cells%20classification.png)

## Training validation loss plots : 

![image alt](https://github.com/jsdfsfw3456/White-blood-cells-classifier/blob/fe98aef0a6a5c2b59535d7636406be5184e6cfcf/training%20and%20%20validation%20loss%20for%20white%20blood%20cells%20classifiaction.png)


## References :
i have  taken the reference  of these papers 
to develop my model :
https://ieeexplore.ieee.org/document/10274670
 
And some other papers 



