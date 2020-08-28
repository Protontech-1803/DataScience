# Implementation of CycleGAN using TensorFlow
This POC trains a model to translate from images from one form to another. For example, horses to zebra using CycleGAN Algorithm. The POC uses a method that can capture the characteristics of one image domain and figure out how these characteristics could be translated into another image domain. The following are steps to implement the same.

Note: [Code used in the POC](https://github.com/Protontech-1803/DataScience/blob/master/CycleGAN/CycleGAN_Code)
1.	Load and prepare the datasets, Split the data into train and test pair to simulate the model as shown below

      ![Alt text](https://github.com/Protontech-1803/DataScience/blob/master/CycleGAN/load_dataset.jpg)
 
2.	Create user defined methods to crop the images to 256X256, normalize the images, create a jitter and to preprocess the training and testing image

      ![Alt text](https://github.com/Protontech-1803/DataScience/blob/master/CycleGAN/resize_image.jpg)
 
3.	Create user defined method to train discriminator and generator.
4.	Create methods to calculate discriminator loss, generator loss, cycle consistency, identity loss and further create methods to create the images and training loop

      ![Alt text](https://github.com/Protontech-1803/DataScience/blob/master/CycleGAN/calculate_loss.jpg)

5.	Initialize the optimizers, update and restore checkpoints for discriminator and generator 
6.	Train the model and save the checkpoints for each iteration

      ![Alt text](https://github.com/Protontech-1803/DataScience/blob/master/CycleGAN/train_model.jpg)

7.	Test the dataset for the trained model.
