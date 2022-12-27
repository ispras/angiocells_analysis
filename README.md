# Description

This is a supplementary repository for AngioCells dataset, which is available at [vessels.ispras.ru](http://vessels.ispras.ru/).
This repository contains assistive scripts for preparing dataset images for training and also for measuring the agreement coefficient between  members of the markup group.

# Installation
To install the scripts, in terminal you need to copy this repository:
```
git clone https://github.com/ispras/angiocells_analysis.git 
```

```bash
cd angiocells_analysis 
```

# Scripts

The repository contains three scripts:

``data_preparation.ipynb`` - allows masks and images to be preprocessed sequentially. 
There are several preparation steps in this notebook:

1. Changing undefined areas in blue. During the markup process, 
the participants encountered difficulties in marking particular areas. 
A separate colour, blue, was chosen for these areas. Later, before training, 
we assigned areas of this colour to areas of the tubes, which produced the highest results. 
It is also possible to experiment and assign these structures to the background area, for example. 
When all masks have only 3 colours displayed, these images can be used to measure the agreement coefficient.

2. Changing the size of the images. The original dataset contains the images and the masks
 marked by the participants. In order to prepare them for training, they need to be resized.

3. Changing the pixels of the masks. All three colors are converted to 0, 1, 2 for 
convenience. The processed masks are saved in the "prepared_dataset" folder.

In total you will have the following folders in the "prepared_dataset" folder:
"images" - ready images for training
"masks" - prepared masks for training
"defined_masks" - ready masks for checking the agreement coefficient

``agreement_measurement.ipynb`` - allows to measure the agreement coefficient between the participants. Pairwise inter-participant agreement was measured using Cohen‘s Kappa statistic. The general form of the equation can be written as:
 
$$
\kappa=\frac{p_0-p_e}{1-p_e}
$$
 
where $p_0$ denotes the observed probability of agreement, and $p_e$ denotes the probability of expected agreement due to chance.  

In the process of receiving the marked dataset, the agreement coefficient was measured several times between the participants. The dataset contains several sub-folders in the "agreement" folder from different measurements. Each of them contains the original photograph from the microscope and the masks of the participants (experts "e" and students "s"). 
To measure the agreement coefficient, you first need to change the blue areas on the masks to a different type of area, which the previous notebook allows you to do. However, the dataset already has ready-made masks for measuring the agreement coefficient, in which the blue areas are marked as tubes. The original masks can be found in the "raw_agreement" folder. Once all the images of interest have been prepared, you can run the script. 

Finally, a folder "results" will appear in your directory, containing both plots of the agreement coefficient between all participants and the tables.

``split_data_to_test_and_train.ipynb`` - Allows the all images to be randomly divided into two sets: 68% for training and 32% for testing. In particular, the training set consists of 77 Good, 36 Dark, 53 Defective, and 19 Different images annotated and sampled for building AI models.