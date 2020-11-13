# Deep-learning-for-in-vivo-near-infrared-imaging

This reposotory is our project for the paper "Deep learning for in vivo near-infrared imaging".  
The code is based on the [original implementation of CycleGAN and pix2pix](https://github.com/junyanz/pytorch-CycleGAN-and-pix2pix). We simplified the code for our task.  

We trained artificial neural networks to transform a fluorescence image in the shorter wavelength NIR window of 900-1300 nm (NIR-I/IIa) to an image resembling a NIR-IIb (1500-1700 nm) image. Details of the experiments can be found in our paper.  

## Instructions
A NIR-I/NIR-IIa fluorescence image can be transformed to a NIR-IIb-like image in the following steps:    
(1) Download the following files and directories from this repository: datasets, generated_image, model directories and all the .py files    
(2) Move the NIR-I/NIR-IIa images to datasets/NIRI_to_NIRII/val/A. The whole-body images we used for training is 640*512 8-bit grayscale images in png format. You might need to resize and crop the images before running the code.    
(3) Install Anaconda (https://www.anaconda.com/products/individual#macos)    
(4) Create a virtual environment by running conda env create -f environment.yml in the command line.    
(5) Activate the virtural environment, and run the code (see "Test the model" for details)

## Model Architecture
CycleGAN:  
![image of CycleGAN](https://github.com/zhuoranzma/Deep-learning-for-in-vivo-near-infrared-imaging/blob/master/figs/CycleGAN.png) 
pix2pix:  
![image of pix2pix](https://github.com/zhuoranzma/Deep-learning-for-in-vivo-near-infrared-imaging/blob/master/figs/pix2pix.png)  


## Dataset
Structure of the dataset:  
```
datasets/  
    NIRI_to_NIRII/  
        train/  
            A  
            B  
        val/  
            A  
            B  
```
A and B contain NIR-I and NIR-IIb images, respectively. To train the model, put your own images in the train directory. To test the model, put the images in the val directory.  
The original wide-field images we used to train the CycleGAN model can be downloaded from datasets.zip. The original light-sheet microscope images we used to train the pix2pix model can be downloaded from lsm_datasets.zip.

## Train the model
To train the CycleGAN model, run:  
```
python train.py --u_net --cuda
```
To train the pix2pix model, run:
```
python pix2pix.py --u_net --cuda
```
parameters will be saved in the model directory. We suggested training the model in a machine with GPU. Alternateively, you can train the model on CPU by removing the --cuda flag. We provided weights of the generator A of our trained models, which can be downloaded from the model directory.

## Test the model
To evaluate the model on the test set, run:
```
python test.py --u_net --cuda
```
Images to be traslated should be stored in the datasets/NIRI_to_NIRII/val/A directory. Images generated by the neural network will be saved in the generated_image directory. We give some examples of our results in the results directory.   


## Acknowledgements
The implementation was inspired by the following implementations in PyTorch: [CycleGAN](https://github.com/junyanz/pytorch-CycleGAN-and-pix2pix) and [CycleGAN](https://github.com/aitorzip/PyTorch-CycleGAN).


