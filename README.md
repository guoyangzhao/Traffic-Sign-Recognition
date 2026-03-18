[![Awesome Logo](https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg)](https://github.com/sindresorhus/awesome)
[![arXiv](https://img.shields.io/badge/arXiv-2509.07996-b31b1b?style=flat-square&logo=arxiv)](https://arxiv.org/)
![Visitors](https://komarev.com/ghpvc/?username=worldbench&repo=awesome-3d-4d-world-models&label=Hello,%20Visitor%20&color=yellow&style=social)
[![PR's Welcome](https://img.shields.io/badge/PRs-welcome-red.svg?style=flat)](https://github.com/guoyangzhao/Traffic-Sign-Recognition/pulls)

# :sunglasses: Traffic Sign Recognition in Autonomous Driving: Dataset, Benchmark, and Field Testing

| <img width="100%" src="doc/fig/teaser.png"> |
|:-:|

This project presents **TS-1M**, a large-scale dataset and diagnostic benchmark for traffic sign understanding.

TS-1M contains over **1M images across 454 categories** with unified annotations and diverse real-world conditions. 
It is designed to evaluate model robustness under **cross-region shifts**, **long-tail distributions**, and **low-clarity scenarios**, while exploring the role of **semantic-enhanced learning**. 
We further validate its practical value by integrating TS-1M into a real autonomous driving system for perception and semantic reasoning.
We organize TS-1M around four key aspects:

| | |
|:-:|:-|
| <img width="120px" src="doc/fig/ts-1m.png"> | **Unified Large-Scale Dataset**. 1M+ images with standardized annotations across 454 categories, providing a consistent foundation for traffic sign recognition. |
| <img width="120px" src="doc/fig/definition.png"> | **Benchmark Across Model Paradigms**. Systematic evaluation of CNNs, transformers, self-supervised, and vision-language models under a unified protocol. |
| <img width="120px" src="doc/fig/icon-challenge.png"> | **Challenge-Oriented Evaluation**. Dedicated subsets for cross-region, rare-class, and low-clarity scenarios enable detailed robustness analysis. |
| <img width="120px" src="doc/fig/icon-real.png"> | **Real-World Validation**. Integration with VLM-based reasoning and 3D mapping demonstrates end-to-end perception-to-decision capability. |
| | |

For more details, kindly refer to our [paper](https://XXX) and [project page](https://guoyangzhao.github.io/projects/ts1m/). :rocket:


### :books: Citation 

If you find this work helpful for your research, please kindly consider citing our papers:
```bib
XXX
```
```bibtex
@inproceedings{zhao2025tsclip,
  title={TSCLIP: Robust CLIP fine-tuning for worldwide cross-regional traffic sign recognition},
  author={Zhao, Guoyang and Ma, Fulong and Qi, Weiqing and Zhang, Chenguang and Liu, Yuxuan and Liu, Ming and Ma, Jun},
  booktitle={2025 IEEE International Conference on Robotics and Automation (ICRA)},
  pages={3846--3852},
  year={2025},
  organization={IEEE}
}
```


### Table of Contents
- [**0. Background**](#background)
  - [Key Challenges](#key-challenges)
  - [Motivation](#motivation)
- [**1. Datasets**](#1-datasets)
  - [TS-1M Datasets](#one-ts-1m-datasets)
  - [Datasets Comparison](#two-datasets-comparison)
- [**2. Modeling**](#2-modeling)
  - [Classic Supervised Models](#one-classic-supervised-models)
  - [Self-Supervised Pretrained Models](#two-self-supervised-pretrained-models)
  - [Vision-Language Models](#three-vision-language-models)
- [**3. Research of Traffic Sign Recognition**](#3-research-of-traffic-sign-recognition)
- [**4. Research of Challenge Task**](#4-research-of-challenge-task)
  - [Cross-Region Recognition](#one-cross-region-recognition)
  - [Rare-Class Recognition](#two-rare-class-recognition)
  - [Low-Clarity Recognition](#three-low-clarity-recognition)
  - [Semantic Understanding](#four-semantic-understanding)
- [**5. Benchmark Results & Analysis**](#5-benchmark-results--analysis)
  - [Main Results](#one-main-results)
  - [Real-World Applications](#two-real-world-applications)
  - [Effect on Autonomous Driving](#three-effect-on-autonomous-driving)
- [**6. Acknowledgements**](#6-acknowledgements)



# Background

| | |
|:-:|:-|
| <img width="600px" src="doc/fig/ts-1m-cover.png"> | Traffic sign recognition plays a critical role in autonomous driving by providing essential cues for navigation and safety. Despite strong performance on standard benchmarks, existing models often struggle to generalize in real-world environments due to distribution shifts and visual variability. |
| | |


## Key Challenges

Real-world TSR remains challenging due to several factors:

- **Regional variation**: sign appearance and standards differ across countries  
- **Long-tail distribution**: many categories have limited samples  
- **Low-clarity conditions**: blur, distance, and occlusion degrade visual quality  
- **Semantic ambiguity**: similar appearances may imply different meanings  

These challenges highlight the gap between benchmark performance and real-world deployment.


## Motivation

Current datasets and evaluations often fail to capture these complexities, making it difficult to assess model robustness in realistic settings.  
A systematic benchmark is therefore needed to evaluate how models behave under distribution shifts, data imbalance, and degraded visual conditions.

| <img width="100%" src="doc/fig/dataset-sample.png"> |
|:-:|





# 1. Datasets

### :one: TS-1M Dataset

TS-1M is a large-scale traffic sign dataset built by integrating multiple public datasets and web-collected samples into a unified benchmark.  
All data are standardized into a consistent taxonomy with **454 classes**, followed by a multi-stage preprocessing pipeline including label normalization, duplicate removal, quality filtering, and manual verification.

<p align="center">
  <img src="doc/fig/dataset-bulid.png" width="100%">
</p>

The final dataset contains **~1.26M images**, with **1.03M for training** and **0.23M for testing**, covering diverse regions and road environments.  
The data distribution follows a realistic **long-tail pattern**, enabling both large-scale recognition and rare-class learning.

<p align="center">
  <img src="doc/fig/dataset-statistics.png" 100="95%">
</p>


### :two: Datasets Comparison

> :timer_clock: In chronological order, from the earliest to the latest.

| Dataset | Region | Classes | Semantic | Examples | Year | Source |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| `STS` | Sverige | 20 | ✓ | 5,582 | 2011 | - |
| `LISA` | America | 47 | ✓ | 7,855 | 2012 | - |
| `GTSRB` | Germany | 43 | ✗ | 51,839 | 2013 | [![Website](https://img.shields.io/badge/Link-yellow?style=flat-square&logo=gitbook)](https://benchmark.ini.rub.de/gtsrb_news.html) |
| `BelgiumTS` | Belgium | 62 | ✗ | 7,125 | 2014 | - |
| `TT100K` | China | 127 | ✗ | 30,000 | 2016 | [![Website](https://img.shields.io/badge/Link-yellow?style=flat-square&logo=gitbook)](https://cg.cs.tsinghua.edu.cn/traffic-sign/) |
| `RTSD` | Russia | 106 | ✗ | 105,509 | 2016 | - |
| `BrazilianTS` | Brazilian | 33 | ✓ | 3,351 | 2018 | - |
| `DFG` | Slovenia | 200 | ✗ | 13,239 | 2019 | [![Website](https://img.shields.io/badge/Link-yellow?style=flat-square&logo=gitbook)](https://www.vicos.si/resources/dfg/) |
| `ARTS` | America | 175 | ✗ | 36,187 | 2019 | - |
| `CanadaTS` | Canada | 39 | ✓ | 204 | 2019 | - |
| `PolishTS` | Polish | 92 | ✗ | 21,044 | 2020 | - |
| `TurkeyTS` | Turkey | 91 | ✗ | 21,249 | 2020 | - |
| `MTSD` | World | 313 | ✓ | 206,388 | 2020 | [![Website](https://img.shields.io/badge/Link-yellow?style=flat-square&logo=gitbook)](https://www.mapillary.com/dataset/trafficsign) |
| `TSCR` | China | 10 | ✗ | 6,348 | 2021 | - |
| `CarlaTS` | Germany | 8 | ✓ | 2,977 | 2021 | - |
| `IndonesiaTS` | Indonesia | 21 | ✓ | 1,800 | 2021 | - |
| `BritishTS` | British | 8 | ✓ | 2,217 | 2021 | - |
| `IndiaTS` | India | 85 | ✓ | 5,726 | 2022 | - |
| `CTSRD` | China | 58 | ✗ | 5,998 | 2023 | - |
| `VNTS` | Vietnam | 51 | ✗ | 7,784 | 2023 | - |
| `BanglaTS` | Bangla | 13 | ✓ | 8,386 | 2023 | - |
| `PTSD` | Iran | 43 | ✓ | 16,421 | 2025 | - |
| **`TS-1M (Train)`** | **World** | **454** | **✓** | **1,033,947** | **2025** | 🚀 *Ours* |
| **`TS-1M (Test)`** | **World** | **454** | **✓** | **233,611** | **2025** | 🚀 *Ours* |




# 2. Modeling

### :one: Classic Supervised Models

> :timer_clock: In chronological order, from the earliest to the latest.

| Model | Paper | Venue | Website | GitHub | 
|:-:|:-|:-:|:-:|:-:|
||
| ResNet-50 / ResNet-101   | [![arXiv](https://img.shields.io/badge/arXiv-1512.03385-b31b1b?style=flat-square&logo=arxiv)](https://arxiv.org/abs/1512.03385) Deep Residual Learning for Image Recognition | CVPR 2016       | -                                                                       | [![GitHub](https://img.shields.io/github/stars/pytorch/vision?style=flat-square&logo=github)](https://github.com/KaimingHe/deep-residual-networks)|
| ResNeXt-50               | [![arXiv](https://img.shields.io/badge/arXiv-1611.05431-b31b1b?style=flat-square&logo=arxiv)](https://arxiv.org/abs/1611.05431) Aggregated Residual Transformations for Deep Neural Networks | CVPR 2017       | -                                                                       | [![GitHub](https://img.shields.io/github/stars/facebookresearch/ResNeXt?style=flat-square&logo=github)](https://github.com/facebookresearch/ResNeXt) |
| ShuffleNetV2             | [![arXiv](https://img.shields.io/badge/arXiv-1807.11164-b31b1b?style=flat-square&logo=arxiv)](https://arxiv.org/abs/1807.11164) ShuffleNet V2: Practical Guidelines for Efficient CNN Architecture Design | ECCV 2018       | -                                                                       | [![GitHub](https://img.shields.io/github/stars/megvii-model/ShuffleNet-Series?style=flat-square&logo=github)](https://github.com/megvii-model/ShuffleNet-Series) |
| MobileNetV3              | [![arXiv](https://img.shields.io/badge/arXiv-1905.02244-b31b1b?style=flat-square&logo=arxiv)](https://arxiv.org/abs/1905.02244) Searching for MobileNetV3 | ICCV 2019       | -                                                                       | [![GitHub](https://img.shields.io/github/stars/pytorch/vision?style=flat-square&logo=github)](https://github.com/pytorch/vision/blob/main/torchvision/models/mobilenetv3.py) |
| EfficientNetV2           | [![arXiv](https://img.shields.io/badge/arXiv-2104.00298-b31b1b?style=flat-square&logo=arxiv)](https://arxiv.org/abs/2104.00298) EfficientNetV2: Smaller Models and Faster Training | ICML 2021       | [![Website](https://img.shields.io/badge/Link-yellow?style=flat-square&logo=gitbook)](https://github.com/google/automl/tree/master/efficientnetv2) | [![GitHub](https://img.shields.io/github/stars/google/automl?style=flat-square&logo=github)](https://github.com/google/automl) |
| ConvNeXt                 | [![arXiv](https://img.shields.io/badge/arXiv-2201.03545-b31b1b?style=flat-square&logo=arxiv)](https://arxiv.org/abs/2201.03545) A ConvNet for the 2020s | CVPR 2022       | -                                                                       | [![GitHub](https://img.shields.io/github/stars/facebookresearch/ConvNeXt?style=flat-square&logo=github)](https://github.com/facebookresearch/ConvNeXt) |
| Vision Transformer (ViT) | [![arXiv](https://img.shields.io/badge/arXiv-2010.11929-b31b1b?style=flat-square&logo=arxiv)](https://arxiv.org/abs/2010.11929) An Image is Worth 16x16 Words: Transformers for Image Recognition at Scale | ICLR 2021       | [![Website](https://img.shields.io/badge/Link-yellow?style=flat-square&logo=gitbook)](https://github.com/google-research/vision_transformer) | [![GitHub](https://img.shields.io/github/stars/google-research/vision_transformer?style=flat-square&logo=github)](https://github.com/google-research/vision_transformer) |
| MobileViT                | [![arXiv](https://img.shields.io/badge/arXiv-2110.02178-b31b1b?style=flat-square&logo=arxiv)](https://arxiv.org/abs/2110.02178) MobileViT: Light-weight, General-purpose, and Mobile-friendly Vision Transformer | ICLR 2022       | -                                                                       | [![GitHub](https://img.shields.io/github/stars/apple/ml-cvnets?style=flat-square&logo=github)](https://github.com/apple/ml-cvnets) |
| EdgeNeXt                 | [![arXiv](https://img.shields.io/badge/arXiv-2206.10589-b31b1b?style=flat-square&logo=arxiv)](https://arxiv.org/abs/2206.10589) EdgeNeXt: Efficiently Amalgamated CNN-Transformer Architecture for Edge Devices | ECCV W 2022     | -                                                                       | [![GitHub](https://img.shields.io/github/stars/mmaaz60/EdgeNeXt?style=flat-square&logo=github)](https://github.com/mmaaz60/EdgeNeXt) |
| SimCLR            | [![arXiv](https://img.shields.io/badge/arXiv-2002.05709-b31b1b?style=flat-square&logo=arxiv)](https://arxiv.org/abs/2002.05709) A Simple Framework for Contrastive Learning of Visual Representations | ICML 2020       | -                                                                       | [![GitHub](https://img.shields.io/github/stars/google-research/simclr?style=flat-square&logo=github)](https://github.com/google-research/simclr) |
| MoCo v3           | [![arXiv](https://img.shields.io/badge/arXiv-2104.02057-b31b1b?style=flat-square&logo=arxiv)](https://arxiv.org/abs/2104.02057) An Empirical Study of Training Self-Supervised Vision Transformers | ICCV 2021       | -                                                                       | [![GitHub](https://img.shields.io/github/stars/facebookresearch/moco-v3?style=flat-square&logo=github)](https://github.com/facebookresearch/moco-v3) |
| DINO             | [![arXiv](https://img.shields.io/badge/arXiv-2104.14294-b31b1b?style=flat-square&logo=arxiv)](https://arxiv.org/abs/2104.14294) Emerging Properties in Self-Supervised Vision Transformers | ICCV 2021       | -                                                                       | [![GitHub](https://img.shields.io/github/stars/facebookresearch/dino?style=flat-square&logo=github)](https://github.com/facebookresearch/dino) |
| MAE              | [![arXiv](https://img.shields.io/badge/arXiv-2111.06377-b31b1b?style=flat-square&logo=arxiv)](https://arxiv.org/abs/2111.06377) Masked Autoencoders Are Scalable Vision Learners | CVPR 2022       | -                                                                       | [![GitHub](https://img.shields.io/github/stars/facebookresearch/mae?style=flat-square&logo=github)](https://github.com/facebookresearch/mae) |
| SimMIM         | [![arXiv](https://img.shields.io/badge/arXiv-2111.09886-b31b1b?style=flat-square&logo=arxiv)](https://arxiv.org/abs/2111.09886) SimMIM: A Simple Framework for Masked Image Modeling | CVPR 2022       | -                                                                       | [![GitHub](https://img.shields.io/github/stars/microsoft/SimMIM?style=flat-square&logo=github)](https://github.com/microsoft/SimMIM) |
| CLIP      | [![arXiv](https://img.shields.io/badge/arXiv-2103.00020-b31b1b?style=flat-square&logo=arxiv)](https://arxiv.org/abs/2103.00020) Learning Transferable Visual Models From Natural Language Supervision | ICML 2021       | -                                                                       | [![GitHub](https://img.shields.io/github/stars/openai/CLIP?style=flat-square&logo=github)](https://github.com/openai/CLIP) |
| BLIP      | [![arXiv](https://img.shields.io/badge/arXiv-2201.12086-b31b1b?style=flat-square&logo=arxiv)](https://arxiv.org/abs/2201.12086) BLIP: Bootstrapping Language-Image Pre-training for Unified Vision-Language Understanding and Generation | ICML 2022       | -                                                                       | [![GitHub](https://img.shields.io/github/stars/salesforce/LAVIS?style=flat-square&logo=github)](https://github.com/salesforce/LAVIS) |
| BLIP-2    | [![arXiv](https://img.shields.io/badge/arXiv-2301.12597-b31b1b?style=flat-square&logo=arxiv)](https://arxiv.org/abs/2301.12597) BLIP-2: Bootstrapping Language-Image Pre-training with Frozen Image Encoders and Large Language Models | ICLR 2023       | -                                                                       | [![GitHub](https://img.shields.io/github/stars/salesforce/LAVIS?style=flat-square&logo=github)](https://github.com/salesforce/LAVIS) |
| LLaVA     | [![arXiv](https://img.shields.io/badge/arXiv-2304.08485-b31b1b?style=flat-square&logo=arxiv)](https://arxiv.org/abs/2304.08485) Visual Instruction Tuning | NeurIPS 2023    | [![Website](https://img.shields.io/badge/Link-yellow?style=flat-square&logo=gitbook)](https://llava-vl.github.io/) | [![GitHub](https://img.shields.io/github/stars/haotian-liu/LLaVA?style=flat-square&logo=github)](https://github.com/haotian-liu/LLaVA) |
||



### :two: Self-Supervised Pretrained Models

> :timer_clock: In chronological order, from the earliest to the latest.

| Model | Paper | Venue | Website | GitHub | 
|:-:|:-|:-:|:-:|:-:|
||
| `GAIA-1` | [![arXiv](https://img.shields.io/badge/arXiv-2309.17080-b31b1b?style=flat-square&logo=arxiv)](https://arxiv.org/abs/2309.17080)<br>GAIA-1: A Generative World Model for Autonomous Driving | arXiv 2023 | [![Website](https://img.shields.io/badge/Link-yellow?style=flat-square&logo=gitbook)](https://wayve.ai/thinking/scaling-gaia-1/) | - |
| `ADriver-I` | [![arXiv](https://img.shields.io/badge/arXiv-2311.13549-b31b1b?style=flat-square&logo=arxiv)](https://arxiv.org/abs/2311.13549)<br>ADriver-I: A General World Model for Autonomous Driving | arXiv 2023 | - | - |
| `Drive-WM` | [![arXiv](https://img.shields.io/badge/arXiv-2311.17918-b31b1b?style=flat-square&logo=arxiv)](https://arxiv.org/abs/2311.17918)<br>Driving into the Future: Multiview Visual Forecasting and Planning with World Model for Autonomous Driving | CVPR 2024 | [![Website](https://img.shields.io/badge/Link-yellow?style=flat-square&logo=gitbook)](https://drive-wm.github.io/) | [![GitHub](https://img.shields.io/github/stars/BraveGroup/Drive-WM)](https://github.com/BraveGroup/Drive-WM) |
||



## :three: Vision-Language Models

> :timer_clock: In chronological order, from the earliest to the latest.

| Model | Paper | Venue | Website | GitHub | 
|:-:|:-|:-:|:-:|:-:|
||
| `MagicDrive3D` | [![arXiv](https://img.shields.io/badge/arXiv-2405.14475-b31b1b?style=flat-square&logo=arxiv)](https://arxiv.org/abs/2405.14475)<br>MagicDrive3D: Controllable 3D Generation for Any-View Rendering in Street Scenes | arXiv 2024 | [![Website](https://img.shields.io/badge/Link-yellow?style=flat-square&logo=gitbook)](https://gaoruiyuan.com/magicdrive3d/) | [![GitHub](https://img.shields.io/github/stars/flymin/MagicDrive3D)](https://github.com/flymin/MagicDrive3D) |
| `DreamForge` | [![arXiv](https://img.shields.io/badge/arXiv-2409.04003-b31b1b?style=flat-square&logo=arxiv)](https://arxiv.org/abs/2409.04003)<br>DreamForge: Motion-Aware Autoregressive Video Generation for Multi-View Driving Scenes | arXiv 2024 | [![Website](https://img.shields.io/badge/Link-yellow?style=flat-square&logo=gitbook)](https://pjlab-adg.github.io/DriveArena/dreamforge/) | [![GitHub](https://img.shields.io/github/stars/PJLab-ADG/DriveArena)](https://github.com/PJLab-ADG/DriveArena) |
||




# 3. Research of Traffic Sign Recognition

> :timer_clock: In chronological order, from the earliest to the latest.

| Model | Paper | Venue | Website | GitHub | 
|:-:|:-|:-:|:-:|:-:|
||
| `SSD` | [![arXiv](https://img.shields.io/badge/arXiv-2301.00527-b31b1b?style=flat-square&logo=arxiv)](https://arxiv.org/abs/2301.00527)<br>Diffusion Probabilistic Models for Scene-Scale 3D Categorical Data | arXiv 2023 | - | [![GitHub](https://img.shields.io/github/stars/zoomin-lee/scene-scale-diffusion)](https://github.com/zoomin-lee/scene-scale-diffusion) |
| `SemCity` | [![arXiv](https://img.shields.io/badge/arXiv-2403.07773-b31b1b?style=flat-square&logo=arxiv)](https://arxiv.org/abs/2403.07773)<br>SemCity: Semantic Scene Generation with Triplane Diffusion | CVPR 2024 | [![Website](https://img.shields.io/badge/Link-yellow?style=flat-square&logo=gitbook)](https://sglab.kaist.ac.kr/SemCity/) |[![GitHub](https://img.shields.io/github/stars/zoomin-lee/SemCity)](https://github.com/zoomin-lee/SemCity) |
| `WoVoGen` | [![arXiv](https://img.shields.io/badge/arXiv-2312.02934-b31b1b?style=flat-square&logo=arxiv)](https://arxiv.org/abs/2312.02934)<br>WoVoGen: World Volume-Aware Diffusion for Controllable Multi-Camera Driving Scene Generation | ECCV 2024 | - | [![GitHub](https://img.shields.io/github/stars/fudan-zvg/WoVoGen)](https://github.com/fudan-zvg/WoVoGen) |
||





# 4. Research of Challenge Task

### :one: Cross-Region Recognition

> :timer_clock: In chronological order, from the earliest to the latest.

| Model | Paper | Venue | Website | GitHub | 
|:-:|:-|:-:|:-:|:-:|
||
| `SSD` | [![arXiv](https://img.shields.io/badge/arXiv-2301.00527-b31b1b?style=flat-square&logo=arxiv)](https://arxiv.org/abs/2301.00527)<br>Diffusion Probabilistic Models for Scene-Scale 3D Categorical Data | arXiv 2023 | - | [![GitHub](https://img.shields.io/github/stars/zoomin-lee/scene-scale-diffusion)](https://github.com/zoomin-lee/scene-scale-diffusion) |
| `WoVoGen` | [![arXiv](https://img.shields.io/badge/arXiv-2312.02934-b31b1b?style=flat-square&logo=arxiv)](https://arxiv.org/abs/2312.02934)<br>WoVoGen: World Volume-Aware Diffusion for Controllable Multi-Camera Driving Scene Generation | ECCV 2024 | - | [![GitHub](https://img.shields.io/github/stars/fudan-zvg/WoVoGen)](https://github.com/fudan-zvg/WoVoGen) |
||



### :two: Rare-Class Recognition

> :timer_clock: In chronological order, from the earliest to the latest.

| Model | Paper | Venue | Website | GitHub | 
|:-:|:-|:-:|:-:|:-:|
||
| `Emergent-Occ` | [![arXiv](https://img.shields.io/badge/arXiv-2210.01917-b31b1b?style=flat-square&logo=arxiv)](https://arxiv.org/abs/2210.01917)<br>Differentiable Raycasting for Self-supervised Occupancy Forecasting | ECCV 2022 | - | [![GitHub](https://img.shields.io/github/stars/tarashakhurana/emergent-occ-forecasting)](https://github.com/tarashakhurana/emergent-occ-forecasting) |
||


### :three: Low-Clarity Recognition

> :timer_clock: In chronological order, from the earliest to the latest.

| Model | Paper | Venue | Website | GitHub | 
|:-:|:-|:-:|:-:|:-:|
||
| `Emergent-Occ` | [![arXiv](https://img.shields.io/badge/arXiv-2210.01917-b31b1b?style=flat-square&logo=arxiv)](https://arxiv.org/abs/2210.01917)<br>Differentiable Raycasting for Self-supervised Occupancy Forecasting | ECCV 2022 | - | [![GitHub](https://img.shields.io/github/stars/tarashakhurana/emergent-occ-forecasting)](https://github.com/tarashakhurana/emergent-occ-forecasting) |
||



### :four: Semantic Understanding

> :timer_clock: In chronological order, from the earliest to the latest.

| Model | Paper | Venue | Website | GitHub | 
|:-:|:-|:-:|:-:|:-:|
||
| `Emergent-Occ` | [![arXiv](https://img.shields.io/badge/arXiv-2210.01917-b31b1b?style=flat-square&logo=arxiv)](https://arxiv.org/abs/2210.01917)<br>Differentiable Raycasting for Self-supervised Occupancy Forecasting | ECCV 2022 | - | [![GitHub](https://img.shields.io/github/stars/tarashakhurana/emergent-occ-forecasting)](https://github.com/tarashakhurana/emergent-occ-forecasting) |
||




# 5. Benchmark Results & Analysis

### :one: Main Results

We benchmark a wide range of models on TS-1M, including classical supervised architectures, self-supervised methods, and vision-language models (VLMs).  

Overall, **vision-language models consistently achieve the best performance**, showing clear advantages over both CNN/Transformer-based models and self-supervised approaches.  
Classical models remain strong baselines, while self-supervised methods provide moderate but less stable improvements.  

These results suggest that **semantic alignment is a key factor** for large-scale and real-world traffic sign recognition.

<p align="center">
  <img src="doc/fig/result-1.png" width="100%">
</p>


### :two: Real-World Applications

We further validate TS-1M in a real autonomous driving setup using a vehicle equipped with **LiDAR and surround-view cameras**.  

A TS-1M fine-tuned **CLIP model** performs traffic sign recognition, while a **LLaVA model** enables scene-level reasoning to infer driving rules.  
The recognized signs are then integrated into the LiDAR map with their **semantic attributes and 3D locations**, forming a structured semantic layer.

This demonstrates that TS-1M supports a practical pipeline from **perception to semantic understanding and map integration**.

<p align="center">
  <img src="doc/fig/real-world.png" width="100%">
</p>


### :three: Effect on Autonomous Driving

TS-1M brings several benefits to autonomous driving systems:

- **Robust recognition in diverse environments** TS-1M-trained models maintain strong performance across diverse environments, including varying road structures and visual conditions.
- **Enhanced semantic understanding beyond classification** By leveraging vision-language models, traffic sign recognition is extended from pure classification to rule-level understanding, enabling more intelligent decision-making.
- **Seamless integration with mapping and planning modules** The integration of recognized signs into LiDAR maps forms a semantic traffic sign layer, supporting downstream tasks such as planning and navigation.

Overall, TS-1M enables the development of **semantics-aware and more reliable autonomous driving systems**.




# 6. Acknowledgements
