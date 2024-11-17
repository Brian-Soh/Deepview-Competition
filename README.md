# Deepview-Competition

This repository contains the submission for Team 6 BBSD (Brian, Benyamin, Sam, and Dennis) for UBC Data Science Club's Deepview Computer Vision Hackathon, held in collaboration with DarkVision. Due to the computational limitations of our shared online notebook, we segmented each step of our pipeline into separate notebooks.

## Pipeline: 
**Data Preprocessing** 
- Extracted the voxel coordinates of the given training ultrasound and mesh files.
- Normalized the ultrasound data points.
- Casted a binary mask to the mesh data points.
- Sliced and resized data to be a 3D array of 256x256x1280.
  
**Model Training**
- Created and trained a Recurrent Residual Convolutional Neural Network with 11 layers (1 input, 9 hidden, 1 output).
- Leveraged Batch Normalization and ReLU activation within the recurrent residual blocks to introduce non-linearity and mitigate the vanishing gradient problem.
- Incorporated downsampling after each encoding layer and upsampling after each encoding layer.

**Reduced Model**
- Trained a reduced version of our model to demonstrate our pipeline due to computational constraints.
- The reduced model was trained on only one training set and for 10 epochs. While it lacks accuracy, it successfully provides estimations and demonstrates our approach.
  
**Prediction Output and Chamfer Distance**
- Applied the same preprocessing steps to the input ultrasound scan as were used for the training set.
- Converted the predicted points into a PLY file.
- Calculated the Chamfer Distance between the predicted output and the correct mesh to assess accuracy.

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
