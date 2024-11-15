# Deepview-Competition

This repository contains the submission for Team 6 BBSD (Brian, Benyamin, Sam, and Dennis) for UBC Data Science Club's Deepview Computer Vision Hackathon which was held in collaboration with Dark Vision. We have included the two notebooks we created for data preprocessing, our model, and Lisa Y. W. Tang's model from a previous iteration of the competition. For additional context, we also included the competition outline and our presentation slide deck.

## Instructions
**Environment Setup:** 
- In the project folder a folder named "raw_files" which will hold the ultrasound scans,  a folder named "train_x" which will hold the processed ultrasound scans, a folder named "train_mesh" which will hold the given meshes, and a folder named "train_y" which will hold the processed meshes.
- Upload the training raw ultrasound scans into raw_files and the training meshes into train_mesh.
Data Preprocessing:
- In the Data Preprocessing Notebook, we could only process one ultrasound scan at a time due to computation limitations. Assign the current scan value (from 1 to 5) to the volume_id variable in the first code block. This will then create .mhd files to process the raw ultrasound scans and preprocess the data and their rotations which will be stored in train_x and train_y respectively as .npy files.

**Model:**
- REQUIREMENT: Must run this line of code in your bash terminal: set PYTHONUTF8=1
- In the Model Notebook we created our model which uses recurrent residual blocks with downsampling and upsampling. We used the binary cross-entropy loss function and the Adam optimizer which are standard for binary classification tasks.
- Our output layer uses a signoid activation function to prodduce a binary mask output which we rebuild into a PLY mesh.
- The notebook takes all .npy files the train_x and train_y folders and reshapes them to include a channel dimension and begins running 25 epochs.

  
**Use Model**
- In the Use Model Notebook, we included a similar preprocessing one for preparing the training ultrasound files.
- The data is then loaded and the model is ran. A 3D array is returned which is then converted into a PLY mesh.
