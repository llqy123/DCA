# Lynamic Context Alignment for Open-Vocabulary Dense Prediction (Under Review)


## Installation

This project is adapted from [OpenCLIP-v2.16.0](https://github.com/mlfoundations/open_clip/tree/v2.16.0). Run the
following command to install the package

```bash
pip install -e . -v
```

## Data Preparation
The main experiments are conducted using images from [COCO](https://cocodataset.org/#home) 
and [LVIS](https://www.lvisdataset.org/) datasets. Please prepare datasets and organize them like the 
following:


```text
LLCS/
├── data
    ├── coco
        ├── annotations
            ├── instances_train2017.json  # the box annotations are not used
            ├── panoptic_val2017.json
            ├── panoptic_val2017     # panoptic masks
        ├── train2017
        ├── val2017
        ├── coco_pseudo_4764.json    # to run RegionCLIP
        ├── coco_proposals.json      # to run LLCS with region proposals
    ├── lvis_v1
        ├── annotations
            ├── lvis_v1_train.json  # the box annotations are not used
        ├── train2017    # the same with coco
        ├── val2017      # the same with coco
```
For LLCS with region proposals or RegionCLIP that uses region-text pairs, obtain `coco_pseudo_4764.json` or `coco_proposals.json` from [Drive](https://drive.google.com/drive/folders/11zG4nJffm0MbvA0Ph19p6jvJFj6VwRAH?usp=sharing). Put the json files under `data/coco`.

## Run
### Original Models 
To run LLCS, first obtain the original models from 
[EVA-02-CLIP](https://github.com/baaivision/EVA/tree/master/EVA-CLIP), and put them under 
`checkpoints/` like the following:

```text
LLCS/
├── checkpoints
    ├── EVA02_CLIP_B_psz16_s8B.pt
    ├── EVA02_CLIP_L_336_psz14_s6B.pt
    
```

For example, if we want to refine ViT-B/16 by LLCS using region proposals on COCO with a different **VFM**, simply run:
```bash
bash scripts/xxx.sh
