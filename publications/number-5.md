---
layout: archive
title: "Lensfree auto-focusing imaging with coarse-to-fine tuning method"
---

### Published on: 06/02/2024 &emsp; in [*Optics and Lasers in Engineering*](https://www.sciencedirect.com/journal/optics-and-lasers-in-engineering)

In this work, we propose a coarse-to-fine tuning method to realize fast and robust lensfree auto-focusing imaging. In our method, a pre-defined simulation-driven focus network (sFocusNet) is constructed to find the coarse estimation of diffractive distances and output the searching range. Then, a new sharpness metric, regularization of gradient (RoG), is constructed with the combination of self-similarity prior and squared gradient map to get the final estimation within the searching range. With the obtained diffractive distances, a multi-height phase retrieval based on plug-and-play regularization is used for final image recovery. The experimental results on different samples are given to show the superiority of our method.

DOI: [10.1016/j.optlaseng.2024.108366](https://doi.org/10.1016/j.optlaseng.2024.108366)

[Supplemental document](../publications/materials/supp_for_sFocusNet.pdf)

Backward Links: [Publications](../_pages/publications.md) / [About Me](../_pages/about.md) / [Research](../_pages/research.md)

# Method Overview

<div align=center><img src="/publications/imgs/sFocusNet/method.png" width=800></div>

**Fig.1** Experimental configuration and workflow of our method. (a) Workflow of coarse-to-fine auto-focusing method. (b) Flowchart of coarse tuning using simulation-driven focus network (sFocusNet). (c) Flowchart of fine tuning using RoG metric.

<div align=center><img src="/publications/imgs/sFocusNet/network.png" width=800></div>

**Fig.2** The architecture of simulation-driven focus network (sFocusNet). (a) Basic architecture. (b) Butterfly transform module. (c) Relative attention module. (d) Feedforward module (FFM). (e) Down-sampling module. The red arrows and symbol ‘*’ denote the skip connection and the butterfly transform, respectively.

<div align=center><img src="/publications/imgs/sFocusNet/data_generate.png" width=450></div>

<div align=center> Fig.3 The flowchart of dataset generation and network training. </div><br/>

<div align=center><img src="/publications/imgs/sFocusNet/ROG.png" width=700></div>

<div align=center> Fig.4 Flowchart of auto-focusing using Regularization of gradient metric (RoG). </div><br/>


# Experimental results

<div align=center><img src="/publications/imgs/sFocusNet/r1.png" width=500></div>

**Fig.5** The auto-focusing results of resolution target. (a) Sharpness curves. (b) is zoomed-in curve from (a) and Ac values are labelled. (c–e) are the back-propagated results by using the estimated distance of 1.02mm, 1.64mm, and 2.00mm.

<div align=center><img src="/publications/imgs/sFocusNet/r2.png" width=500></div>

**Fig.6** The auto-focusing results of testis of fish. (a) The sharpness curves of the captured intensity at the first height. (b) is the magnified curve from the red box in (a). (c–e) are reconstructed by the estimated distances of Group I, Group II, and Group III. (f–j) are expanded regions cropped from (c–e).

<div align=center><img src="/publications/imgs/sFocusNet/r3.png"></div>

<div align=center> Table.1 The auto-focusing performance summary of subjective assessment for 20 types of samples. </div><br/>

<div align=center><img src="/publications/imgs/sFocusNet/r4.png"></div>

<div align=center> Table.2 The summary of accuracy criterion values (Ac) for 20 types of samples. </div><br/>

<div align=center><img src="/publications/imgs/sFocusNet/r5.png"></div>

<div align=center> Table.3 The summary of resolution criterion values (Rc) for 20 types of samples. </div><br/>

<div align=center><img src="/publications/imgs/sFocusNet/r6.png" width=750></div>

**Fig.7** Coarse distance estimation of 20 types of samples by using different frequency-domain simulation-driven networks. (a–e), (f–j), and (k–o) are focusing error plots with the training step size from 0.03mm to 0.07mm for SE-ResNet, MobileNetV3, and sFocusNet, respectively.

<div align=center><img src="/publications/imgs/sFocusNet/r7.png"></div>

<div align=center> Table.4 The comparison of running time for different metrics. </div><br/>

<div align=center><img src="/publications/imgs/sFocusNet/r8.png" width=700></div>

**Fig.8** The generalization validation of our method on new commercial pathological slides and new imaging sensor. (a) The used three commercial pathological slides. (b) is the focusing error plot of the new recorded experimental datasets for our sFocusNet. (c–e) are auto-focusing curves by using coarse-to-fine tuning. (f–h) are retrieved amplitude images of the three slides using the estimated distances from (c–e).

<div align=center><img src="/publications/imgs/sFocusNet/r9.png" width=750></div>

**Fig.9** The auto-focusing performance by using cross-validation for frequency-domain experiment-driven networks. (a–c) are focusing error plots of three networks when the paired datasets from one sample are used for training. (d–f) are focusing error plots of three networks when the paired datasets from two samples are used for training.

<div align=center><img src="/publications/imgs/sFocusNet/r10.png" width=450></div>

<div align=center> Table.5 Performance comparison of different experiment-driven networks for Fig.9 </div><br/>

# Conclusion

In this paper, we have proposed a coarse-to-fine method, realizing fast and robust auto-focusing imaging for lensfree on-chip microscopes. 20 sets of samples are firstly used to prove that RoG metric outperforms other metrics with high robustness, accuracy, and unimodality. Then, the fast positioning of sFocusNet is proved and the running time of distance estimation can be decreased to ~4s for our method. Finally, new three commercial slides and a new CMOS sensor are used to conduct the extended experiment, which proves that our method shows better generalization than experiment-driven networks. We believe that our method will offer a practical auto-focusing solution for the commercialization of lensfree microscopes.
