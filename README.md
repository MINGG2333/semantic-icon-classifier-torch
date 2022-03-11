# Semantic Icon Classifier pytorch version

A CNN based model classifying 99 icon classes appear most often in Android apps. Sometimes, we have input images that do not belong to any of the 99 classes, either can be a random image or a very rarely used icon class. Therefore, we develop an extra Anomaly detector to handle this case. Our work is presented in the paper "Learning Design Semantics for Mobile Apps".

## Requirements
```
pytorch
matplotlib
scikit-learn
scipy==1.2.1
...
```

## Download data

1. ``data/``: [(Download)](https://drive.google.com/open?id=1SiD_U5ifjX1poJZzLB-MwvoUQBhutYzH)


What is inside:
```
training_x.npy: training icons (requires for both train and test evaluation)

training_y.npy: training labels (requires for both train and test evaluation)

validation_x.npy: testing icons (requires for both train and test evaluation)

validation_y.npy: testing labels (requires for both train and test evaluation)

validation_metadata.json: meta information about each icon (require for both train and test evaluation)

anomalies_embeddings.npy:

gmm_invalid_class.npy:

gmm_valid_class.npy:

x_train_class.npy:

y_train_embeddings.npy:

```

2. ``pyt_model.pt``: [(Download)](https://drive.google.com/file/d/1cy1wcMQIDElLlUF2OWOkL9UU0Jp_OCEA/view?usp=sharing)

3. `icon.zip`: [(Optional for testing, Download)](https://drive.google.com/file/d/1D0CFmDP0xNSyfSkK7kUHnfP0HnpcKZc1)
You do not need this zip file in training a model. In the evaluation, you may need these raw icon images when passing an argument flag  ``--save_images``  to generate a testing sample. The generated file is stored in JSON. **Warning**: Over 100k of image files, becareful aftre you unzip it.

## How to train our icon classifier

#### Step 1

Unzip `data.zip` in the current directory.

Create a folder ``saved_models``, put ``pyt_model.pt`` here.

#### Step 2

```
python cnn_pretrain.py
```

When training is finish, you will see the following message printed in the terminal:

```
Accuracy on test data is: 94.22
Macro precision
0.8700204788608547
Macro recall
0.8603409627700631
```
These results are evaluated without anomaly detector. 


## Evaluate your icon classifier from a saved model

#### Evaluate without anomaly detection
```
python cnn_pretrain.py --model_path ./saved_models/pyt_model.pt
```

#### predict an icon without anomaly detection (support CPU)
```
python cnn_pretrain.py --model_path ./saved_models/pyt_model.pt -i 251272.png
```

#### Evaluate with anomaly detection (not support now)
```
python cnn_pretrain.py --anomaly --model_path ./saved_models/small_cnn_weights_100_512.h5
```

## Notes
* You can change any hyperparameters in `settings.py`. 
* Our default CNN training epoch is `100`.

## Contributions
* Paper: [Learning Design Semantics for Mobile Apps](http://interactionmining.org/rico)

## If you have any question, please contact:
* Jason Situ (junsitu2@illinois.edu)
