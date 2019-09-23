# STEM-Simulation-Images
This repo contains the code which can generate simulated STEM images as training sets in deep learning
## Generating Training Set
This part will show you why we need generate simualted STEM images as training set of deep learning model and how to use these code generate and process these images.
### Purpose
In deep learning, whether people can get a good model always depends on the amounts and quality of their training set. While in nano-scale, especially for electron microscope images, there are no specific images sets for training DL models. If people want to use deep learning to recognize features, like point defects in electron microscope images, how to get enough high quality, labeled training image is the key question. In previous work, researchers in EM field use several methods to get training set, including manually labeling and using fourier filter to label features. But these methods are time consuming or unaccurate. Here we come up a method to generate large amount simulated STEM images with high quality labels to train DL models.
Our method is based on computem written by Earl J. Kirkland, which is used for Transmission Electron Microscope Image Simulation. With computem people can get single high quality EM images, our purpose is to batchly generate EM images and its defect maps for training. You can find the computem code [here](https://sourceforge.net/projects/computem/)
### How to use the code.
The code used for generating training sets hase two parts: the first part is used for generate .xyz and .param files, which can be input into computem to get simulate images and defect labels, the second part is used to add noises on simulated images to make them more "realistic".
#### First Part: Gererate .xyz files and .param files
In computem, people need input two files to get one simulated STEM image. One is .xyz file, whihc cantains atoms' positions and .params contains microscope conditions. Through changing .xyz file, people can add random defects in the material, like point defects and through .param file, people can change different EM conditions, like amount of electron dose on images. 
#### Second Part: Post Process on Raw simulate images
If we compare real STEM images and simulated images from computem, we can easily distiguish them because there are more complex noise features in real STEM image. So before we use simulated images, we need add more features to make the simulated images "more real".
In the post process, we add shear, constrain to simulate the sample draft under STEM and rotations to simulate different lattice orientation. The random gaussian noise and ununiform backgroud are also added to create complex noise feature.
### Some deep learning examples we use simulated images as training set
#### Find different points in 2D materials.
To train a deep learning model to locate different points in WSeTe, we use this code generate ADF-STEM images of with defects, including vacancies and doping atoms in metal and chacaugon site. The defects are randomly distribute in the images and we can generate both the STEM images and the defect maps at the same time. Here are the samples of the simulated images and its comparation with the real images.
The deep leaning model trained only on the simulated images can have more than 95% accuracy in the real STEM images on defect prediction.
The result is published here
