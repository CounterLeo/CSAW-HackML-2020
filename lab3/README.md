# Lab 3


```bash
├── lab3
    └── data 
        └── cl
            └── valid.h5 // this is clean validation data used to design the defense
            └── test.h5  // this is clean test data used to evaluate the BadNet
        └── bd
            └── bd_valid.h5 // this is sunglasses poisoned validation data
            └── bd_test.h5  // this is sunglasses poisoned test data
    └── models
        └── bd_net.h5
        └── bd_net.h5
        └── model_prune_2.h5
        └── model_prune_4.h5
        └── model_prune_10.h5
        └── model_prune_30.h5
    └── architecture.py
    └── eval.py // this is the evaluation script
```

## I. Dependencies
   1. Python 3.6.9
   2. Keras 2.3.1
   3. Numpy 1.16.3
   4. Matplotlib 2.2.2
   5. H5py 2.9.0
   6. TensorFlow-gpu 1.15.2

## II. Data
   1. Download the validation and test datasets from [here](https://drive.google.com/drive/folders/1Rs68uH8Xqa4j6UxG53wzD0uyI8347dSq?usp=sharing) and store them under `data/` directory.
   2. The dataset contains images from YouTube Aligned Face Dataset. We retrieve 1283 individuals and split into validation and test datasets.
   3. bd_valid.h5 and bd_test.h5 contains validation and test images with sunglasses trigger respectively, that activates the backdoor for bd_net.h5. 
  

## III. Evaluating the Backdoored Model
   1. The DNN architecture used to train the face recognition model is the state-of-the-art DeepID network. 
   2. To evaluate the backdoored model, execute `eval.py` by running:  
      `python3 eval.py <clean test data directory> <poisoned test data directory> <model directory>`.
      E.g., `python3 eval.py data/cl/valid.h5 data/bd/bd_valid.h5 models/bd_net.h5`. This will output:
      Clean Classification accuracy: 98.64 %
      Attack Success Rate: 100 %

## IV. Evaluating the repaired Models
1. The repaired models are saved and uploaded under folder `lab3/models`, they are```model_prune_2.h5, model_prune_4.h5, model_prune_10.h5, and model_prune_30.h5 ```. You could run them by `eval.py` as instructed above.. 
2. The results evaluated by these repaired models are below:

|  Repaired Model B' | Clean Classification Accuracy | Attack Success Rate |
|:------------------:|:-----------------------------:|:-------------------:|
|  model_prune_2.h5  |       95.90023382696803       |        100.0        |
|  model_prune_4.h5  |       92.29150428682775       |  99.98441153546376  |
|  model_prune_10.h5 |       84.54403741231489       |  77.20966484801247  |
|  model_prune_30.h5 |       54.762275915822286      |   6.96024941543258  |    

## V. Important Notes
Please use only clean validation data (valid.h5) to design the pruning defense. And use test data (test.h5 and bd_test.h5) to evaluate the models. 
