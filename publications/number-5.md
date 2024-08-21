---
layout: archive
title: "Lensfree auto-focusing imaging with coarse-to-fine tuning method"
---

### Published on: 06/02/2024 &emsp; in [*Optics and Lasers in Engineering*](https://www.sciencedirect.com/journal/optics-and-lasers-in-engineering)


In this work, we propose a coarse-to-fine tuning method to realize fast and robust lensfree auto-focusing imaging. In our method, a pre-defined simulation-driven focus network (sFocusNet) is constructed to find the coarse estimation of diffractive distances and output the searching range. Then, a new sharpness metric, regularization of gradient (RoG), is constructed with the combination of self-similarity prior and squared gradient map to get the final estimation within the searching range. With the obtained diffractive distances, a multi-height phase retrieval based on plug-and-play regularization is used for final image recovery. The experimental results on different samples are given to show the superiority of our method. $\hat{\omega_n}$

DOI: [10.1016/j.optlaseng.2024.108366](https://doi.org/10.1016/j.optlaseng.2024.108366)

[Supplemental document](../publications/materials/supp_for_sFocusNet.pdf)

Backward Links: [Publications](../_pages/publications.md) / [About Me](../_pages/about.md) / [Research](../_pages/research.md)

# Method

In our method, a simulation-driven focus network (sFocusNet) is designed as a coarse tuning to decrease the distance searching range, and then a regularization of gradient (RoG) metric is constructed as a fine tuning to achieve an accurate estimation. In this section, each part of our method will be introduced in details.

## Method Overview

As shown in Fig. 1(a), we apply our method in a multi-height lensfree on-chip platform to realize auto-focusing imaging. In our method, a set of intensity patterns are captured at different heights and then processed by our method to output the real diffractive distances. As shown in Fig.1(b) and (c), our method is composed of coarse tuning and fine tuning.

### Coarse Tuning

In the coarse tuning, a simulation-driven focus network (sFocusNet) is constructed to get a coarse position of the focusing distance. The sFocusNet consists of Rel-attention module and butterfly transform, in which a natural image dataset is introduced in a lensfree diffraction degradation process to generate distance-to-image pairs for model training.

### Fine Tuning

In the fine tuning step, the distance searching range obtained from the coarse tuning is employed, and a new sharpness metric (RoG), is constructed to find the sharpest image of back-propagated images within the searching range. Finally, a multi-height phase retrieval with plug-and-play regularization is used for final image recovery.

<div align=center><img src="/publications/imgs/sFocusNet/method.png" width=800></div>

**Fig.1** Experimental configuration and workflow of our method. (a) Workflow of coarse-to-fine auto-focusing method. (b) Flowchart of coarse tuning using simulation-driven focus network (sFocusNet). (c) Flowchart of fine tuning using RoG metric.

## Simulation-driven focus network (sFocusNet)

### Architecture of sFocusNet

The architecture of our simulation-driven network is shown in Fig. 2. As shown in Fig. 2(a), the overall network is formulated by butterfly transform, relative attention, feedforward, and down-sampling modules, which are stacked and cascaded into five stages, i.e., S0, S1, S2, S3, and S4. From S0 to S4, the image resolution decreases to half of the preceding stage, and the number of channels increases.

The basic structures of butterfly transform, Rel-Attention, feedforward, and down-sampling modules are shown in Fig. 2(b–e), respcetively. 
+ The butterfly transform convolution layer (BFTConv1x1) uses a pointwise convolution with a kernel size of 1x1xM, aggregating the feature map from the previous layer in a depthwise manner to produce a new feature map.
+ The Rel-Attention module is built based on the self-attention mechanism, which linearly decomposes the input into three matrices: Query, Key, and Value, and then computes the output using dynamic weights.
+ The FFM module linearly transforms data through fully connected layers and introduces non-linear mapping using the GELU activation function.

<div align=center><img src="/publications/imgs/sFocusNet/network.png" width=800></div>

**Fig.2** The architecture of simulation-driven focus network (sFocusNet). (a) Basic architecture. (b) Butterfly transform module. (c) Relative attention module. (d) Feedforward module (FFM). (e) Down-sampling module. The red arrows and symbol ‘*’ denote the skip connection and the butterfly transform, respectively.

### Dataset Generation

As shown in Fig. 3(a), the detail of simulated dataset generation can be generalized as follows:

1. 13 photographic images with a size of 3000×3000, including plant, animal, and landscape, are selected and normalized as the amplitude image \\((A)\\) of the object, and the corresponding phase images are produced by setting \\(P = \quad \pi (1 − A)\\),where \\( \quad \\) is a random value from 0 to 0.5.
2.  the obtained wavefield of the object \\((Ae^{iP})\\) is forward propagated by angular spectrum model with a set of diffractive distances to generate multi-distance intensity patterns \\( W_n \\)
3.  The intensity patterns (3000×3000×N ×13) are cropped into a mass of image patches \\( \hat{\omega_n} \\) with a size of 224×224 pixels.

<div align=center><img src="/publications/imgs/sFocusNet/data_generate.png" width=450></div>

<div align=center> Fig.3 The flowchart of dataset generation and network training. </div><br/>

## Regularization of gradient metric (RoG)

<div align=center><img src="/publications/imgs/sFocusNet/ROG.png" width=700></div>

<div align=center> Fig.4 Flowchart of auto-focusing using Regularization of gradient metric (RoG). </div><br/>


# Experimental results

## RoG validation

### Resolution target

<div align=center><img src="/publications/imgs/sFocusNet/r1.png" width=500></div>

**Fig.5** The auto-focusing results of resolution target. (a) Sharpness curves. (b) is zoomed-in curve from (a) and Ac values are labelled. (c–e) are the back-propagated results by using the estimated distance of 1.02mm, 1.64mm, and 2.00mm.

### Pathological slide

<div align=center><img src="/publications/imgs/sFocusNet/r2.png" width=500></div>

**Fig.6** The auto-focusing results of testis of fish. (a) The sharpness curves of the captured intensity at the first height. (b) is the magnified curve from the red box in (a). (c–e) are reconstructed by the estimated distances of Group I, Group II, and Group III. (f–j) are expanded regions cropped from (c–e).

<div align=center><img src="/publications/imgs/sFocusNet/r3.png"></div>

<div align=center> Table.1 The auto-focusing performance summary of subjective assessment for 20 types of samples. </div><br/>

<div align=center><img src="/publications/imgs/sFocusNet/r4.png"></div>

<div align=center> Table.2 The summary of accuracy criterion values (Ac) for 20 types of samples. </div><br/>

## sFocusNet validation

<div align=center><img src="/publications/imgs/sFocusNet/r5.png" width=750></div>

**Fig.7** Coarse distance estimation of 20 types of samples by using different frequency-domain simulation-driven networks. (a–e), (f–j), and (k–o) are focusing error plots with the training step size from 0.03mm to 0.07mm for SE-ResNet, MobileNetV3, and sFocusNet, respectively.

<div align=center><img src="/publications/imgs/sFocusNet/r6.png" width=450></div>

<div align=center> Table.3 Performance comparison of different simulation-driven networks for Fig.7. </div><br/>

<div align=center><img src="/publications/imgs/sFocusNet/r7.png"></div>

<div align=center> Table.4 The comparison of running time for different metrics. </div><br/>

## Validation on the network generalization

<div align=center><img src="/publications/imgs/sFocusNet/r8.png" width=700></div>

**Fig.8** The generalization validation of our method on new commercial pathological slides and new imaging sensor. (a) The used three commercial pathological slides. (b) is the focusing error plot of the new recorded experimental datasets for our sFocusNet. (c–e) are auto-focusing curves by using coarse-to-fine tuning. (f–h) are retrieved amplitude images of the three slides using the estimated distances from (c–e).

<div align=center><img src="/publications/imgs/sFocusNet/r9.png" width=750></div>

**Fig.9** The auto-focusing performance by using cross-validation for frequency-domain experiment-driven networks. (a–c) are focusing error plots of three networks when the paired datasets from one sample are used for training. (d–f) are focusing error plots of three networks when the paired datasets from two samples are used for training.

<div align=center><img src="/publications/imgs/sFocusNet/r10.png" width=450></div>

<div align=center> Table.5 Performance comparison of different experiment-driven networks for Fig.9. </div><br/>

# Conclusion

In this paper, we have proposed a coarse-to-fine method, realizing fast and robust auto-focusing imaging for lensfree on-chip microscopes. 20 sets of samples are firstly used to prove that RoG metric outperforms other metrics with high robustness, accuracy, and unimodality. Then, the fast positioning of sFocusNet is proved and the running time of distance estimation can be decreased to ~4s for our method. Finally, new three commercial slides and a new CMOS sensor are used to conduct the extended experiment, which proves that our method shows better generalization than experiment-driven networks. We believe that our method will offer a practical auto-focusing solution for the commercialization of lensfree microscopes.
