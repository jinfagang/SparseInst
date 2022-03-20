<div align="center">
<h1>SparseInst &#128640;</h1>
<span><font size="4", >A simple framework for real-time instance segmentation, CVPR 2022</font></span>
</br>
by
<br>
Tianheng Cheng, <a href="https://xinggangw.info/">Xinggang Wang</a><sup><span>&#8224;</span></sup>, Shaoyu Chen, Wenqiang Zhang, Qian Zhang, Chang Huang, Zhaoxiang Zhang, Wenyu Liu
</br>
(<span>&#8224;</span>: corresponding author)

<!-- <div><a href="">[Project Page]</a>(comming soon)</div>  -->
<div><a href="">[Paper]</a></div>

</div>

---

## Overview
We propose a conceptually novel, efficient, and fully convolutional framework for real-time instance segmentation. Previously, most instance segmentation methods heavily rely on object detection and perform mask prediction based on bounding boxes or dense centers. In contrast, we propose a sparse set of instance activation maps, as a new object representation, to highlight informative regions for each foreground object. Then instance-level features are obtained by aggregating features according to the highlighted regions for recognition and segmentation. Moreover, based on bipartite matching, the instance activation maps can predict objects in a one-to-one style, thus avoiding non-maximum suppression (NMS) in post-processing. Owing to the simple yet effective designs with instance activation maps, SparseInst has extremely fast inference speed and achieves 40 FPS and 37.9 AP on the COCO benchmark, which significantly outperforms the counterparts in terms of speed and accuracy.

<center>
<img src="./resources/sparseinst.png">
</center>


### Highlights 

* SparseInst presents a new object representation method, *i.e.*, Instance Activation Maps (IAM), to adaptively localize objects.
* SparseInst is a simple and fully convolutional framework without attention, iteratively structures, or non-maximum suppression (NMS). 
* SparseInst achieves good trade-off between speed and accuracy.

## Updates

*This project is under active development, please stay tuned!*

* [2022-3-20] We have released the code and models for SparseInst! 
 

## Models

We provide two versions of SparseInst, *i.e.*, the basic IAM (3x3 convolution) and the Group IAM (G-IAM for short), with different backbones.
All models are trained on MS-COCO *train2017*.

#### Fast models

| model | backbone | input | aug | AP<sup>val</sup> |  AP  | FPS | weights |
| :---- | :------  | :---: | :-: |:--------------: | :--: | :-: | :-----: |
| [SparseInst](configs/sparse_inst_r50_base.yaml) | [R-50]() | 640 | &#x2718; | 32.8 | - | 44.3 | [model](https://drive.google.com/file/d/12RQLHD5EZKIOvlqW3avUCeYjFG1NPKDy/view?usp=sharing) |
| [SparseInst](sparse_inst_r50vd_base.yaml) | [R-50-vd](https://github.com/rwightman/pytorch-image-models/releases/download/v0.1-weights/resnet50d_ra2-464e36ba.pth) | 640 | &#x2718; | - | - | - | [model]()|
| [SparseInst (G-IAM)](configs/sparse_inst_r50_giam.yaml) | [R-50]() | 608 | &#x2718; | 33.4 | - | 44.6 | [model](https://drive.google.com/file/d/1pXU7Dsa1L7nUiLU9ULG2F6Pl5m5NEguL/view?usp=sharing) |
| [SparseInst (G-IAM)](configs/sparse_inst_r50_giam_aug.yaml) | [R-50]() | 608 | &#10003; | 34.2 | 34.7 | 44.6 | [model](https://drive.google.com/file/d/1MK8rO3qtA7vN9KVSBdp0VvZHCNq8-bvz/view?usp=sharing) |
| [SparseInst (G-IAM)](configs/sparse_inst_r50_dcn_giam_aug.yaml) | [R-50-DCN]() | 608 | &#10003;| 36.4 | 36.8 | 41.6 | [model](https://drive.google.com/file/d/1qxdLRRHbIWEwRYn-NPPeCCk6fhBjc946/view?usp=sharing) |
| [SparseInst (G-IAM)](configs/sparse_inst_r50vd_giam_aug.yaml) | [R-50-vd](https://github.com/rwightman/pytorch-image-models/releases/download/v0.1-weights/resnet50d_ra2-464e36ba.pth) | 608 | &#10003;| 35.6 | 36.1 | 42.8| [model](https://drive.google.com/file/d/1dlamg7ych_BdWpPUCuiBXbwE0SXpsfGx/view?usp=sharing) |
| [SparseInst (G-IAM)](configs/sparse_inst_r50vd_dcn_giam_aug.yaml) | [R-50-vd-DCN](https://github.com/rwightman/pytorch-image-models/releases/download/v0.1-weights/resnet50d_ra2-464e36ba.pth) | 608 | &#10003; | 37.4 | 37.9 | 40.0  | [model](https://drive.google.com/file/d/1clYPdCNrDNZLbmlAEJ7wjsrOLn1igOpT/view?usp=sharing)|
| [SparseInst (G-IAM)](sparse_inst_r50vd_dcn_giam_aug.yaml) | [R-50-vd-DCN](https://github.com/rwightman/pytorch-image-models/releases/download/v0.1-weights/resnet50d_ra2-464e36ba.pth) | 640 | &#10003; | 37.7 | 38.1 | 39.3 |  [model](https://drive.google.com/file/d/1clYPdCNrDNZLbmlAEJ7wjsrOLn1igOpT/view?usp=sharing)| 


<!-- #### Larger models

| model | backbone | input | AP<sup>val</sup> |  AP  | FPS | weights |
| :---- | :------ | :---: | :--------------: | :--: | :-: | :-----: |
| SparseInst (G-IAM) | [R-101]() | 640 |                   |      |   | [model]()| -->


**Note:** 
* *We will continue adding more models* including more efficient convolutional networks, vision transformers, and larger models for high performance and high speed, please stay tuned &#128513;!
* Inference speeds are measured on one NVIDIA 2080Ti.
* We haven't adopt TensorRT or other tools to accelerate the inference of SparseInst. However, we are working on it now and will provide support for ONNX, TensorRT, and [Blade](https://github.com/alibaba/BladeDISC) as soon as possible!
* AP denotes AP evaluated on MS-COCO *test-dev2017*
* *input* denotes the shorter side of the input, *e.g.*, 512x864 and 608x864, we keep the aspect ratio of the input and the longer side is no more than 864.
* The inference speed might slightly change on different machines (2080 Ti) and different versions of detectron (we mainly use [v0.3](https://github.com/facebookresearch/detectron2/tree/v0.3)). If the change is sharp, e.g., > 5ms, please feel free to contact us.
* For `aug` (augmentation), we only adopt the simple random crop (crop size: [384, 600]) provided by detectron2.

## Installation and Prerequisites

This project is built upon the excellent framework [detectron2](https://github.com/facebookreseach/detectron2), and you should install detectron2 first, please check [official installation guide](https://detectron2.readthedocs.io/en/latest/tutorials/install.html) for more details.

**Note:** we mainly use [v0.3](https://github.com/facebookresearch/detectron2/tree/v0.3) of detectron2 for experiments and evaluations. Besides, we also test our code on the newest version [v0.6](https://github.com/facebookresearch/detectron2/tree/v0.6). If you find some bugs or incompatibility problems of higher version of detectron2, please feel free to raise a issue!

Install the detectron2:

```bash
git clone https://github.com/facebookresearch/detectron2.git
# if you swith to a specific version, e.g., v0.3 (recommended)
git checkout tags/v0.3
# build detectron2
python setup.py build develop
```

## Getting Start


### Testing SparseInst

Before testing, you should specify the config file `<CONFIG>` and the model weights `<MODEL-PATH>`. In addition, you can change the input size by setting the `INPUT.MIN_SIZE_TEST` in both config file or commandline.

* [Performance Evaluation] To obtain the evaluation results, *e.g.*, mask AP on COCO, you can run:

```bash
python train_net.py --config-file <CONFIG> --num-gpus <GPUS> --eval MODEL.WEIGHTS <MODEL-PATH>
# example:
python train_net.py --config-file configs/sparse_inst_r50_giam.yaml --num-gpus 8 --eval MODEL.WEIGHTS sparse_inst_r50_giam_aug_2b7d68.pth
```

* [Inference Speed] To obtain the inference speed (FPS) on one GPU device, you can run:

```bash
python test_net.py --config-file <CONFIG> MODEL.WEIGHTS <MODEL-PATH> INPUT.MIN_SIZE_TEST 512
# example:
python test_net.py --config-file configs/sparse_inst_r50_giam.yaml  --eval MODEL.WEIGHTS sparse_inst_r50_giam_aug_2b7d68.pth INPUT.MIN_SIZE_TEST 512
```

**Note:** 
* The `test_net.py` only supports **1 GPU** and **1 image per batch** for measuring inference speed.
* The inference time consists of the *pure forward time* and the *post-processing time*. While the evaluation processing, data loading, and pre-processing for wrappers (*e.g.*, ImageList) are not included.
* `COCOMaskEvaluator` is modified from [`COCOEvaluator`](https://github.com/facebookresearch/detectron2/blob/main/detectron2/evaluation/coco_evaluation.py) for evaluating mask-only results.


### Training SparseInst

To train the SparseInst model on COCO dataset with 8 GPUs. 8 GPUs are required for the training. If you only have 4 GPUs or GPU memory is limited, it doesn't matter and you can reduce the batch size through `SOLVER.IMS_PER_BATCH` or reduce the input size. If you adjust the batch size, learning schedule should be adjusted according to the linear scaling rule.

```bash
python train_net.py --config-file <CONFIG> --num-gpus 8 
# example
python train_net.py --config-file configs/sparse_inst_r50vd_dcn_giam_aug.yaml --num-gpus 8
```


## Acknowledgements


SparseInst is based on [detectron2](https://github.com/facebookresearch/detectron2), [OneNet](https://github.com/PeizeSun/OneNet), [DETR](https://github.com/facebookresearch/detr), and [timm](https://github.com/rwightman/pytorch-image-models), and we sincerely thanks for their code and contribution to the community!


## Citing SparseInst

If you find SparseInst is useful in your research or applications, please consider giving us a star &#127775; and citing SparseInst by the following BibTeX entry.

```BibTeX
@inproceedings{Cheng2022SparseInst,
  title     =   {Sparse Instance Activation for Real-Time Instance Segmentation},
  author    =   {Cheng, Tianheng and Wang, Xinggang and Chen, Shaoyu and Zhang, Wenqiang and Zhang, Qian and Huang, Chang and Zhang, Zhaoxiang and Liu, Wenyu},
  booktitle =   {Proc. IEEE Conf. Computer Vision and Pattern Recognition (CVPR)},
  year      =   {2022}
}

```


## License

SparseInst is released under the [MIT Licence](LICENCE).