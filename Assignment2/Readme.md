## EVA 4 Phase 2 Assignment 2 Deploy Trained Mobilenet_v2 on AWS
------------------------------------------------------------------------------------------------------------

## Group : 
1. Abhijit Mali
2. Gunjan Deotale
3. Sanket Maheshwari
4. Pratik Jain

----------------------
## Notes 
---------------------------------------------------------------------------------------------------------------------------

# what model did you train?
Following is the Pytorch based implementation to use pretrained Mobilenetv2 model and train it over four classes namely Flying Birds, Winged_drones, Large Quadcopters, Small Quadcopters. The images for these labels can be found out at
https://drive.google.com/file/d/133nsp1_PJXUpKOLzcYu9JivzHlGKMr8x/view?usp=sharing

The model is deployed on aws and working is tested on Insomnia using url
https://9nnncm80a9.execute-api.ap-south-1.amazonaws.com/dev/classify

# Resizing Strategy:
Although the images were of different sizes, we have used image resizing in albumentation to resize to 256x256 and then we used image cropping in albumentation to crop it to 224x224 as this size is need as input to Mobilenet v2.

# Explain the code?
We added following two fully connected model on top of existing pretrained model. For training we have freezed all existing layers until average pool and unfreezed newly added last 2 layers.
# Mobilenet Model Addition to suit new class addition
![](Readme_images/Model_add.png)

Main colab file is kept at
https://github.com/gdeotale/E4P2/blob/master/Assignment2/Mobilenet_Training/Main.ipynb

New Generated model is kept at 
https://github.com/gdeotale/E4P2/blob/master/Assignment2/Mobilenet_Training/Generated_models/Modeljit.pt

Training/Testing method is kept at
https://github.com/gdeotale/E4P2/blob/master/Assignment2/Mobilenet_Training/Train_Test_utils/

We have used Albumentation as method of augmentation, we tried image resizing, Image cropping, Cut Out and Image Normalization as methods in Augmentation
Image Augmentation and Dataloader is kept at
https://github.com/gdeotale/E4P2/blob/master/Assignment2/Mobilenet_Training/Main.ipynb

We have segregated the data in train test folder in ratio of 70:30 classwise.

The model has been trained over 50 epochs and we are able to achive 85% as top test accuracy.

# Plots
![](Readme_images/Plots.png)
# LR vs Epochs
![](Readme_images/lr_vs_epoch.png)
# Confusion Matrix
![](Readme_images/confusion_matrix.jpeg)
# Misclassified Images
![](Readme_images/misclassification_library.jpeg)
# Cloud Watch Logs
![](Readme_images/CloudWatch.png)
# Api Gateway
![](Readme_images/ApiGateway.png)


# Result from the API:

   **Input Image :**
  
   ![bird](https://user-images.githubusercontent.com/25937235/89651641-dfab2d00-d8e1-11ea-90aa-f2dc88aeb6ac.jpeg)
  
   **Prediction :**
  
   <img width="276" alt="Screenshot 2020-08-07 at 7 14 01 PM" src="https://user-images.githubusercontent.com/25937235/89651838-2ac54000-d8e2-11ea-9147-da0d111b2853.png">
  
   **Input Image :**
    
   ![Small-Quadcopter](https://user-images.githubusercontent.com/25937235/89652343-fb630300-d8e2-11ea-92d5-22d20a18c3f0.jpg)
    
   **Prediction :**
    
   <img width="303" alt="Screenshot 2020-08-07 at 7 20 17 PM" src="https://user-images.githubusercontent.com/25937235/89652388-09188880-d8e3-11ea-9530-1582176177e5.png">
   
   **Input Image :**
   
   ![large-quadcopter](https://user-images.githubusercontent.com/25937235/89652847-b8555f80-d8e3-11ea-82d0-3accbbfd2693.jpg)
   
   **Prediction :**
   
   <img width="313" alt="Screenshot 2020-08-07 at 7 25 04 PM" src="https://user-images.githubusercontent.com/25937235/89652839-b55a6f00-d8e3-11ea-936a-9ce6462dd818.png">
   
   **Input Image :**
   
   ![Winged-Drone](https://user-images.githubusercontent.com/25937235/89652990-f81c4700-d8e3-11ea-8420-19e8c42aba53.jpg)
   
   **Prediction :**
   
   <img width="290" alt="Screenshot 2020-08-07 at 7 26 55 PM" src="https://user-images.githubusercontent.com/25937235/89652984-f6eb1a00-d8e3-11ea-87b3-3ea68b16769c.png">

  


