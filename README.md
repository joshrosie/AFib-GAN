# AFIB-GAN

### MLECG
### Joshua Rosenthal 
*RSNJOS005*

The AFib-GAN codebase is completely run using Jupyter Notebooks and is coupled with Google Colab Pro + and Google Drive. While we will provide ipynb files, it is important to note that this code is built to be used with Colab Pro +. These codebases are interactive but there are detailed use cases which will abstract many function calls for smoother usage.

This readme serves as a general overview of how the codebases work. The codebases themselves have much more detailed instructions on how to run them.

For all codebases, please ensure that you have permission to use Google Drive with Colab as datasets, generators, and folds are fed into and out of codebases through Drive.

I have provided the set of assets that I used for my thesis. Assets range from presaved augmneted dataset splits for cross-validation, to generators for augmnetation.

Find all presaved assets here:
https://drive.google.com/drive/folders/1wovyO357d0k4DaAjPT1QnRSfUjSY4kO6?usp=sharing

Please move this folder into Drive and ensure that it is not contained in any other directories. Note that whenever you run a codebase you must grant access to Google Drive.

If running on Colab is an issue, I have also made the presaved assets available for download. Please download the folder from Drive and save it into this directory. Since the folder is very large it will be downloaded in segments. Please consiolidate all segments into one folder called 'pre\_saved\_assets'. Once that is done and is saved in this directory, you can activate the virtual environment and install the prerequisites by running the following commands in a prompt: 
```
source venv/bin/activate

pip install -r requirements.txt
```
Be sure to change the type of tensorflow you need to install depending on your OS. This can be done by looking in the requirments folder and commenting out the tensorflow that will not be compatible with your OS. Once done, please ensure all note books are running in the virtual environment. To do this in VSCode, at the top right of your screen, you will see: 
```
base(Python 3.9.2)
```
If you click on this icon, a list of alternative environments will be displayed. Select the one that looks like:
```
venv(Python 3.10.6)
```

# Links to Colab Codebase
Before running any code, please ensure that GPU usage is enabled. Use this tutorial (https://www.tutorialspoint.com/google_colab/google_colab_using_free_gpu.htm) if you do not know how to enable it.

There are 3 codebases:
 
 ***All experiments run during my thesis have used these note books***

1. preprocessing.ipynb : 
   
   https://colab.research.google.com/drive/1e7qqywGjrYFfVmf5vlJTtV1PtPI_UKKr?usp=sharing

2. GAN.ipynb : 
   
   https://colab.research.google.com/drive/1RTMFgeI8X0Kchjicr6fd0OHqGZzmaskL?usp=sharing

3. classifier.ipynb

    https://colab.research.google.com/drive/1b38zrwvoWTGgBm_PwrP2Sp_XGu9Ixfhg?usp=sharing

These should be viewed and run in the order displayed above. As mentioned earlier, this code is originally built to run using Google Colab and thus many of the libraries used will be of versions supplied by Colab.

If you have any additional queires please email them to me at: rnsjos005@myuct.ac.za

# Preprocessing

This class has two main functions
1. Splitting the dataset
2. Creating the image set to be used with the GAN and Classifier

The key outcomes of this class are two image datasets: One for training and cross-validation, and another to be used as a holdout experiment.

The ipynb note books have documentation on how to run each codebase. Here we offer a general overview on how to run this particular codebase. 

### Important
Before looking at the use cases please run the following cells:
- Prerequisites
- Splitting
- Preprocessing

### Use Cases
There are 2 use cases
1. Make datasets from scratch
2. Make datasets from presaved splits

To run either use case simply run the cell corresponding to the desired use case.

There is an added functionality to download the datasets to your device or to add the folder to the pre_saved_assets directory. To do either you can simply run the code whose headings correspond to the appropriate actions.

# GAN

This codebase houses:
- The Generative Adversarial Networks
- The custom training loops
- Image set generation for image quality assesments

The prupose of this codebase is to train the generative models. The key outcomes of this are a saved trained generator to be used in augmentation techniques and a small synthetic dataset to be used in image quality assesments.

### Important
Before looking ate the use cases please run the following cells:
- Prerequisites
- Models
- TrainGAN

### Use Cases
In this subfolder you will first see a helper function 
```
def load_grayscale_images(dir, in_shape = (128,128), batch_size = 64)
```
Please run this cell.

This subfolder contains all the experiments run in my thesis.
1. AFib-GAN
2. WCGAN
3. WCGANGP-RMSprop
4. WCGANGP-Adam

You will also find functionality for saving a small image set for the computation KID and FID as well as functionality to save the generator. All of these objects will be automatically transfered to the pre_saved_assets folder.

# Classfier

This codebase is the grounds for evaluating the GAN both directly through image quality assesments and indirectly through augmentation. As such this codebase has two functions:
1. Augmentation Experiments
2. Image quality assesments

As ipynb files are interactive, several code blocks need to be run by hand.

### Before running experiments
Please run the following cells:
- Prerequisites
- Model
- Data Loader
- Cross Validation

## Usecases
At the bottom you will find two predefined use cases:
1. Cross Validation
2. Image Quality
### Cross Validation

Upon opening this folder you will see the following line:
```
!unzip /content/gdrive/MyDrive/pre_saved_assests/splits_for_classifier.zip &> /dev/nul
```
This line must be run as it fetches the unseen test holdout set. This also fetches the precomputed folds for cross validation.

You will then see a header asking to select a set of assets you want to use for experimentation
- DCCGAN
- WCGAN
- WCGANGP-RMSprop
- WCGANGP-Adam

Simply run the code cell corresponding to the GAN you want to assess.

After this you will find a header asking you how you want to run cross validation. There are two options. You can either run from precalculated folds or you can create the folds using a pretrained generator (the nature of which will correspond to the assets you imported) to augment the training set.

### Image Quality
Running this cell will require you to restart Colab since clean-fid requires a different version of PIL. Running this cell will calculate the FID and KID of a small dataset generated by a particular architecture - the choice of which is determined by the assets you chose to import.

It is important to note here that the poor performance of the classifier (even though the image quality of the GAN is relatively high) is likely due to the low resolution of images

# Acknowledgments
Without the help of my supervisors: Deshen Moodley and Mbithe Nzomo, as well of the support of my peers: Shai Aarons and Jarred Fisher, this project would have never come to fruition. Thank you.