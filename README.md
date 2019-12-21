# Detection and Classification of breast cancer in slide images

Project description: Detection and classification of breast cancer metastases in whole-slide images of histological lymph node sections.

Presentation video link: (https://storage.googleapis.com/dl4cv1445/ADL/LuLiuPresentation.mp4)          
Github repo link: (https://www.anaconda.com/distribution/)

## Setup

### Prerequisites
- Linux or OSX
- NVIDIA GPU or simply running on Colab

## Walk through

- Dataobtain_all.ipynb: Obtain all the output patches when sliding a 128 x 128 window across .tif file.(*id_im.npy: index of all patches that do not have cancer, *id_ma.npy: index of all patches that have cancer)

   ```
    - dt001.zip
     - 001_0_1.jpg
     - 001_0_1_mask.jpg
     ...
    -index
      - 001id_im.npy
      - 001id_ma.npy
      ...
    ```
- Dataclean.ipynb: Create a `slide.npy` and `mask.npy` that contains all index of patches extracted from .tif file ranging from `001.tif` to `110.tif` after implementing a train_test_split.

- Segmentation.ipynb: Create a modified Unet to solve the segmentation problem based on the input images and mask images of the tumor over the slide images (zoom level 5).

- Classification_generator.ipynb: Create a model to solve the classification problem based on the input images and created labels. (zoom level0, level1, level3)

- Concatenation.ipynb: Prediction evaluation and visualization of the prediction of the current model from extracted patches with different zoom levels.
 ```
 - model_tumor_level0.h5 (classification):
   - model based on images from zoom level 0
   - 94.73% accuracy and loss 0.525
 - model_tumor_level1.h5 (classification):
   - model based on images from zoom level 1
   - 96.29% accuracy and loss 0.518
 - model_tumor_level3.h5 (classification):
   - model based on images from zoom level 3
   - 97% accuracy and loss 0.512
 - model_tumor_level5.h5 (segmentation):
   - model based on images from zoom level 5
   - 97% accuracy and loss 0.512

- Concatenation2.ipynb: Use 3 pretrained model: model_tumor_level0.h5, model_tumor_level1.h5, model_tumor_level3.h5 to extract the features from pictures from different zoom levels and build a model to make a prediction on whether there is tumor in image with the smallest zoom level.
