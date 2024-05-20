# Background-remover-for-photos

Skills - UNet, Semantic Segmentation, Deep Learning, Machine Learning
Tools - Tensorflow API modelling of ML, Python

This project is aimed at being able to remove the background from images , where by foreground I mean humans

## Dataset -

Image mask pairs built from images taken from tiktok - https://www.kaggle.com/datasets/tapakah68/segmentation-full-body-tiktok-dancing-dataset

## Approach - 

I will train a UNet which will be able to generate masks for humans in a picture , and then using the masks I can easily apply computer vision based operations to replace the areas in actual photo corresponding to not a human (i.e. background parts) and replace it with Black .

## Model Structure - 

I have trained a UNet for this segmentation problem. Its structure looks like - 

![image](https://github.com/ayush-agarwal-0502/background-remover-for-photos/assets/86561124/fc49e365-7ba4-4942-8742-7f90073cc6f4)

You can read the original research paper for UNET at - https://arxiv.org/pdf/1505.04597 .

For exact structure of the model I have trained , u can see the png image I have added in this repo - .

## Results - 

Pure model outputs (where each pixel is output of a sigmoid function) - 

![image](https://github.com/ayush-agarwal-0502/background-remover-for-photos/assets/86561124/6de72c46-4afd-4418-9a77-40c953a237d8)
![image](https://github.com/ayush-agarwal-0502/background-remover-for-photos/assets/86561124/7184fb12-f15b-4f9b-bd4a-41d49220d396)
![image](https://github.com/ayush-agarwal-0502/background-remover-for-photos/assets/86561124/06405894-1fc3-43b6-938a-31aa53b91ae9)

Outputs after applying a threshold to the UNet outputs - 

![image](https://github.com/ayush-agarwal-0502/background-remover-for-photos/assets/86561124/6dc01a89-6d51-4473-80b8-19f46b0ff7fd)
![image](https://github.com/ayush-agarwal-0502/background-remover-for-photos/assets/86561124/877f7e6b-5175-4e53-bb37-8e14696bf14f)
![image](https://github.com/ayush-agarwal-0502/background-remover-for-photos/assets/86561124/b3984951-504a-40bd-b55f-dda039580fc4)


## Other details - 

It required about 30 minutes of training on Kaggle notebooks GPU .

Best lesson learnt - there is usually more background than foreground in these images , so we have to use a custom loss function which gives more weightage to foreground . Initially when I trained without weighted loss , I just got blank images from the UNet but was getting very good accuracy . Which goes to the show that accuracy is not a good metric for binary classification problems .

Oh and by the way , only loss affects the training process of a tensorflow model , metric is just for observation purposes . 

