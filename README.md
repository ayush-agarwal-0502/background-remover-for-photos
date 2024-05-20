# Background-remover-for-photos

Skills - UNet, Semantic Segmentation, Deep Learning, Machine Learning
Tools - Tensorflow API modelling of ML, Python

This project is aimed at being able to remove the background from images , where by foreground I mean humans. This could be useful in photos when we need to change the background. 

Future work could involve using blob detecting algorithms to detect different humans in mask , then removing one of them by filling that area of mask with black . Alternatively , we could crop out a person from actual photo using the mask and then we could use GANs to fill it thus becoming the background people remover for photos which is a feature in new phone cameras . 

## Dataset -

Image mask pairs built from images taken from tiktok - https://www.kaggle.com/datasets/tapakah68/segmentation-full-body-tiktok-dancing-dataset

## Approach - 

I will train a UNet which will be able to generate masks for humans in a picture , and then using the masks I can easily apply computer vision based operations to replace the areas in actual photo corresponding to not a human (i.e. background parts) and replace it with Black .

## Model Structure - 

I have trained a UNet for this segmentation problem. Its structure looks like - 

![image](https://github.com/ayush-agarwal-0502/background-remover-for-photos/assets/86561124/fc49e365-7ba4-4942-8742-7f90073cc6f4)

You can read the original research paper for UNET at - https://arxiv.org/pdf/1505.04597 .

For exact structure of the model I have trained , u can see the png image I have added in this repo - https://github.com/ayush-agarwal-0502/background-remover-for-photos/blob/main/unet_model.png .

## Results - 

Pure model outputs (where each pixel is output of a sigmoid function) - 

![image](https://github.com/ayush-agarwal-0502/background-remover-for-photos/assets/86561124/6de72c46-4afd-4418-9a77-40c953a237d8)
![image](https://github.com/ayush-agarwal-0502/background-remover-for-photos/assets/86561124/7184fb12-f15b-4f9b-bd4a-41d49220d396)
![image](https://github.com/ayush-agarwal-0502/background-remover-for-photos/assets/86561124/06405894-1fc3-43b6-938a-31aa53b91ae9)
![image](https://github.com/ayush-agarwal-0502/background-remover-for-photos/assets/86561124/b315e790-0e2c-4bf9-8616-59415cc95940)
![image](https://github.com/ayush-agarwal-0502/background-remover-for-photos/assets/86561124/6cb459d3-5eb1-448b-9844-af9773271d06)


Outputs after applying a threshold to the UNet outputs - 

![image](https://github.com/ayush-agarwal-0502/background-remover-for-photos/assets/86561124/6dc01a89-6d51-4473-80b8-19f46b0ff7fd)
![image](https://github.com/ayush-agarwal-0502/background-remover-for-photos/assets/86561124/877f7e6b-5175-4e53-bb37-8e14696bf14f)
![image](https://github.com/ayush-agarwal-0502/background-remover-for-photos/assets/86561124/b3984951-504a-40bd-b55f-dda039580fc4)


## Other details - 

It required about 30 minutes of training on Kaggle notebooks GPU (which I had to do multiple times as I am not an expert)

Best lesson learnt - there is usually more background than foreground in these images , so we have to use a custom loss function which gives more weightage to foreground . Initially when I trained without weighted loss , I just got blank images from the UNet but was getting very good accuracy . Which goes to the show that accuracy is not a good metric for binary classification problems .

Oh and by the way , only loss affects the training process of a tensorflow model , metric is just for observation purposes . 

Another good learning from this project - In tensorflow, we can build models using sequential or functional API way . Sequential modelling only works for basic models without branches and stuff . SO we have to use Tensorflow functional API for this model . 

Warning - if you use my model weights directly, it might not import directly due to custom loss function , so try compile=False, then copy my loss function, then compile the model manually 

Another learning - we can set persistance = files and variables in kaggle notebooks while using save and run to save the outputs 
