# Deepview-Competition

This repository contains the submission for Team 6 BBSD (Brian, Benyamin, Sam, and Dennis) for UBC Data Science Club's Deepview Computer Vision Hackathon which was held in collaboration with Dark Vision. Due to the computational limitations of our online shared notebook, we segmented each step of our pipeline into seperate notebooks.

## Pipeline: 
**Data Preprocessing** 
- Extracted the voxel coordinates of the given training ultrasound and mesh files.
- Normalized our ultrasound data points.
- Casted a binary mask on over our mesh data points.
- Sliced and resized data to be a 3D array of 256x256x1280.
  
**Model Training**
- Created and trained a Recurrent Convolutional Neural Network with 11 layers (1 input, 9 hidden, 1 output).
- Used Batch Normalization and ReLU activation within our recurrent blocks to introduce non-linearity into our model and avoid the vanishing gradient problem.
- Downsampling after each encoding layer and Upsampling after each encoding layer.

**Reduced Model**
- Due to our limitations in computing capacity, we trained a reduced model to fully demonstrate our pipeline.
- The reduced model was trained on only 1 training set and 10 epochs, hence it lacks accuracy but is still able to plot out estimations.
  
**Prediction Output and Chamfer Distance**
- We apply the same preprocessing to the input ultrasound scan as we did for the training set
- Converted our predicted points into a PLY file
- Calculated the chamfer distance between the predicted output and the correct mesh to access accuracy

## Instructions
**Environment Setup:** 
- In the project folder a folder named "raw_files" which will hold the ultrasound scans,  a folder named "train_x" which will hold the processed ultrasound scans, a folder named "train_mesh" which will hold the given meshes, and a folder named "train_y" which will hold the processed meshes.
- Upload the training raw ultrasound scans into raw_files and the training meshes into train_mesh.

**Data Preprocessing:**
- In the Data Preprocessing Notebook, we could only process one ultrasound scan at a time due to computation limitations. Assign the current scan value (from 1 to 5) to the volume_id variable in the first code block. This will then create .mhd files to process the raw ultrasound scans and preprocess the data and their rotations which will be stored in train_x and train_y respectively as .npy files.

**Model:**
- REQUIREMENT: Must run this line of code in your bash terminal: set PYTHONUTF8=1
- NOTE: We faced obstacles in training our model as it demands significant computational resources to train, hence we have attached a "reduced version" which serves as a proof of concept for our pipeline. This Reduced Model was only trained off of one ultrasonic scan and one mesh. Expectedly, it lacks accuracy but still generates a mesh.
- In the Model Notebook we created our model which uses recurrent residual blocks with downsampling and upsampling. We used the binary cross-entropy loss function and the Adam optimizer which are standard for binary classification tasks.
- Our output layer uses a signoid activation function to prodduce a binary mask output which we rebuild into a PLY mesh.
- The notebook takes all .npy files the train_x and train_y folders and reshapes them to include a channel dimension and begins running 25 epochs.
  
**Use Model**
- In the Use Model Notebook, we included a similar preprocessing one for preparing the training ultrasound files.
- The data is then loaded and the model is ran. A 3D array is returned which is then converted into a PLY mesh.
