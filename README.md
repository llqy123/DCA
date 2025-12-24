## Installation

This project is adapted from [OpenCLIP-v2.16.0](https://github.com/mlfoundations/open_clip/tree/v2.16.0). Run the
following command to install the package

```bash
pip install -e . -v -i https://pypi.tuna.tsinghua.edu.cn/simple
```

## Data Preparation
The main experiments are conducted using images from [COCO](https://cocodataset.org/#home) 
and [LVIS](https://www.lvisdataset.org/) datasets. Please prepare datasets and organize them like the 
following:


```text
CLIPSelf/
├── data
    ├── coco
        ├── annotations
            ├── instances_train2017.json  # the box annotations are not used
            ├── panoptic_val2017.json
            ├── panoptic_val2017     # panoptic masks
        ├── train2017
        ├── val2017
        ├── coco_pseudo_4764.json    # to run RegionCLIP
        ├── coco_proposals.json      # to run CLIPSelf with region proposals
    ├── lvis_v1
        ├── annotations
            ├── lvis_v1_train.json  # the box annotations are not used
        ├── train2017    # the same with coco
        ├── val2017      # the same with coco
```
For CLIPSelf with region proposals or RegionCLIP that uses region-text pairs, obtain `coco_pseudo_4764.json` or `coco_proposals.json` from [Drive](https://drive.google.com/drive/folders/11zG4nJffm0MbvA0Ph19p6jvJFj6VwRAH?usp=sharing). Put the json files under `data/coco`.

## Run
### Original Models 
To run CLIPSelf, first obtain the original models from 
[EVA-02-CLIP](https://github.com/baaivision/EVA/tree/master/EVA-CLIP), and put them under 
`checkpoints/` like the following:

```text
CLIPSelf/
├── checkpoints
    ├── EVA02_CLIP_B_psz16_s8B.pt
    ├── EVA02_CLIP_L_336_psz14_s6B.pt
    
```

### Training and Testing 
We provide the scripts to train CLIPSelf and RegionCLIP under [scripts/](scripts), they are summarized as follows:

For example, if we want to refine ViT-B/16 by CLIPSelf using only image patches on COCO, simply run:
```bash
bash scripts/train_clipself_coco_image_patches_eva_vitb16.sh

bash scripts/train_clipself_coco_region_proposals_eva_vitb16.sh

```
We also provide the checkpoints of the listed experiments above in [Drive](https://drive.google.com/drive/folders/1APWIE7M5zcymbjh5OONqXdBOxFy3Ghwm?usp=sharing). 
And they can be organized as follows:

```text
CLIPSelf/
├── checkpoints
    ├── eva_vitb16_coco_clipself_patches.pt     # 1
    ├── eva_vitb16_coco_clipself_proposals.pt   # 2
    ├── eva_vitb16_coco_regionclip.pt           # 3
    ├── eva_vitl14_coco_clipself_patches.pt     # 4
    ├── eva_vitl14_coco_clipself_proposals.pt   # 5
    ├── eva_vitl14_coco_regionclip.pt           # 6
    ├── eva_vitb16_lvis_clipself_patches.pt     # 7
    ├── eva_vitl14_lvis_clipself_patches.pt     # 8
```

To evaluate a ViT-B/16 model, run:
```bash
bash scripts/test_eva_vitb16_macc_boxes_masks.sh name_of_the_test path/to/checkpoint.pt
```
To evaluate a ViT-L/14 model, run:
```bash
bash scripts/test_eva_vitl14_macc_boxes_masks.sh name_of_the_test path/to/checkpoint.pt
```

## F-ViT
Go to the folder `CLIPSelf/F-ViT` and follow the instructions in this [README](F-ViT/README.md).

## License
This project is licensed under [NTU S-Lab License 1.0](LICENSE).

## Citation

```bibtex

```


## Acknowledgement

We thank [OpenCLIP](https://github.com/mlfoundations/open_clip/tree/v2.16.0), 
[EVA-CLIP](https://github.com/baaivision/EVA/tree/master/EVA-CLIP) and 
[MMDetection](https://github.com/open-mmlab/mmdetection/tree/v2.28.1) for their valuable code bases.
