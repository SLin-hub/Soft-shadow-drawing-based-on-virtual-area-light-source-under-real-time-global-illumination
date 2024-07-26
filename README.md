# Soft shadow drawing based on virtual area light source under real-time global illumination

# 项目配置

* 首先克隆本项目到本地 git lfs clone git@github.com:AngelMonica126/GraphicAlgorithm.git（**注意用到 git lfs clone指令，因为部分模型太大了放在LFS上面**）

* 下载GraphicSDK https://pan.baidu.com/s/1XjYGrGhCO_KSqL7pCUzBrA 密码: 1234 ，然后将其解压即可

* 用**管理员的权限**运行GraphicSDK里面的 Graphic.bat 以自动配置环境变量

* 在克隆好的项目中点击setup.bat生成vs环境（默认生成VS2017，可以用文本格式打开setup.bat用你自己的vs版本替代vs2017保存即可）

* 在项目中选择Frame点击生成以生成动态链接库

* 然后就可以运行其他的项目了~

# Model preparation
We need three scene model data: Sponza, Gallery, and Vokselia_Spaw.

Download the Sponza dataset from [here](https://sketchfab.com/3d-models/the-picture-gallery-231fdb3e9e354c6faaa3c250f8c9988f);

Download the Sponza model data according to the [tutorial](https://github.com/alexgkendall/SegNet-Tutorial/tree/master/CamVid);

Download the ADE20K dataset from [webpage](https://groups.csail.mit.edu/vision/datasets/ADE20K/).


## Requirements

pytorch >= 1.2.0
apex
opencv-python


# Model Checkpoint

## Pretrained Models

Baidu Pan Link: https://pan.baidu.com/s/1s_BdU9PzMTpZoGJtCJZeEA  extract code(p24v)


# Training

Our resnet-101-based methods including fcn, u-net, deeplabv3+, pspnet can be trained by 8-4090-TI gpus with batchsize 8.
Our training contains two steps:

## 1, Train the base model.
    We found 150-180 epoch is good enough for warm up traning.
```bash
sh ./scripts/train/train_cityscapes_Resnet-101_Transformer_dual_branch.sh
```

## 2, Re-Train with our module with lower LR using pretrained models.


### For Transformer_dual_branch:
  You can use the pretrained ckpt in previous step.
  

# Evaluation


## 1, Single-Scale Evaluation
```bash
sh ./scripts/evaluate_val/eval_cityscapes_Resnet-101_Transformer_dual_branch.sh 
```

## 2, Multi-Scale Evaluation
```bash
sh ./scripts/evaluate_val/eval_cityscapes_Resnet-101_Transformer_dual_branch_ms.sh
```
## 3, Evaluate F-score on Segmentation Boundary.(change the path of snapshot)
```bash
sh ./scripts/evaluate_boundy_fscore/evaluate_cityscapes_deeplabv3_r101_decouple
```

# Submission on Cityscapes

You can submit the results using our checkpoint by running 

```bash
sh ./scripts/submit_tes/submit_cityscapes_ResNet101_Transformer_dual_branch.sh
```

# Demo 
Here we give some demo scripts for using our checkpoints.
You can change the scripts according to your needs.

```bash
python ./test.py
```
