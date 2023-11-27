# VSCNet
## Overview
This project includes source codes and examples of VSCNet. 

For quick start of using VSCNet, we provide runnable testing examples, including pretrained models(in ./model_save), a sub-hierarchy(in ./hierarchy), and several samples(in ./data_food101_demo) from testing set of Ingredient-101.
## Environment
* Pytorch >= 1.10.2
* Python >= 3.6.5
* torchvision >= 0.2.1
## Examples
We provide some examples to demonstrate the mechanism of VSCNet.

    python test.py --result_path result/ --hierarchy_path hierarchy/ --art_epoch 2

Here is one of the cases: classifying an image with ground-truth label **1** by the global model (Visual backbone) outputs the **wrong Top-1 prediction**, while the correct prediction is at **Top-4**. After refinement, the model finally outputs the **correct Top-1 prediction**.

> Sample 0, Ground Truth label: 1

> Top-1 Class prediction: Global model: [20], HAF: [1], HCG: [1] | final prediction: [1]

> Top-2 Class prediction: Global model: [77], HAF: [1], HCG: [50]

> Top-3 Class prediction: Global model: [38], HAF: [77], HCG: [20]

> Top-4 Class prediction: Global model: [1], HAF: [1], HCG: [23]

> Top-5 Class prediction: Global model: [42], HAF: [1], HCG: [77]


## Training
We also provide training codes for reproduction. Please refer to [option](./opts.py) to see more parameters.
### Pre-leaning hierarchical knowledge base
####
Training **ARL model** for associating visual-semantic pairs and creating **Knowledge base**.

    python train_offline.py --result_path result/ --hierarchy_path [PATH_HIERARCHY] --art_epoch [EPOCH_OF_CLUSTER] --net_v [BACKBONE]
### Training HCG-based Classification model
Training **HCG**.

    python train_oneline.py --result_path result/ --hierarchy_path [PATH_HIERARCHY] --art_epoch [EPOCH_OF_CLUSTER] --net_v [BACKBONE]
## Testing
    python test.py --hierarchy_path [PATH_HIERARCHY] --art_epoch [EPOCH_OF_CLUSTER] --net_v [BACKBONE]
