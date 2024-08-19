---
layout: archive
title: "Lensfree auto-focusing imaging using nuclear norm of gradient"
---

## Published in: 04/10/2022 &emsp; on [*Optics and Lasers in Engineering*](https://www.sciencedirect.com/journal/optics-and-lasers-in-engineering)

Backward Links: [Publications](../_pages/publications.md)

Auto-focusing is an essential task for lensfree holographic microscopy, where the optimal focal plane needs to be determined from refocused Z-stack data. In this work, we propose a new auto-focusing criterion, nuclear norm of gradient (NoG), to enhance the accuracy of distance estimation for lensfree imaging. 

The NoG metric is composed of three parts: shape acquisition, gradient calculation, and gradient fusion. The experiment is conducted in a multi-height on-chip system, where 20 sets of samples including resolution target, stained slide, and label-free cell are employed. The experimental results demonstrate that the accuracy of the NoG metric on auto-focusing is superior to state-of-the-art metrics. Also, the experiment of a multi-layer target proves that the NoG metric has a good optical-sectioning capability. We believe that the NoG metric is expected to be a useful tool for lensfree on-chip microscopes.

DOI: [10.1016/j.optlaseng.2022.107076](https://doi.org/10.1016/j.optlaseng.2022.107076)

# Method Overview

<div align=center><img src="/publications/imgs/NOG/NOG_auto.png" width=700></div>

<div align=center> Fig.1 The experimental system and flowchart of auto-focusing strategy. </div><br/>

<div align=center><img src="/publications/imgs/NOG/NOG.png" width=700></div>

<div align=center> Fig.2 The flowchart of the NoG metric. </div><br/>

# Experimental Results

<div align=center><img src="/publications/imgs/NOG/NOG_r1.png" width=400></div>

Fig.3 The auto-focusing results of resolution target. (a) Captured hologram. (b) Auto-focusing curve. (c–e) The reconstructed targets by the backpropagation method with the estimated distance of 1.35 mm, 1.06 mm, and 1.05 mm.

<div align=center><img src="/publications/imgs/NOG/NOG_r2.png" width=400></div>

Fig.4 The auto-focusing result of pixel super-resolved resolution target. (a)Auto-focusing curve. (b–d) The econstructed targets by the back-propagation method with the estimated distance of 0.710 mm, 0.717 mm, and 0.726 mm.

<img src="/publications/imgs/NOG/T1.png">

<div align=center> Table.1 The summary of auto-focusing results for 20 sets of samples. </div>

Backward Links: [Publications](../_pages/publications.md)
