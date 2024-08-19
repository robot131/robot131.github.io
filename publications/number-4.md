---
layout: archive
title: "Dual-constrained physics-enhanced untrained neural network for lensless imaging"
---

### Published on: 01/05/2024 &emsp; in [*Journal of the Optical Society of America A*](https://opg.optica.org/josaa/home.cfm)

In this paper, we proposed a dual-constrained physics-enhanced untrained neural network (termed DPENet) for lensless imaging. Compared to the current untrained network, our method adopts the single-channel generative model for phase update and imposes the regularized optimization for amplitude update, which effectively keeps the consistency of the two channels and avoids the unstable inference of a complex-valued wavefield. Experimental results are given to validate our method.

DOI: [10.1364/JOSAA.510147](https://doi.org/10.1364/JOSAA.510147)

[Supplemental document](../publications/materials/supp_for_DPENet.pdf)

Backward Links: [Publications](../_pages/publications.md) / [About Me](../_pages/about.md) / [Research](../_pages/research.md)

# Method Overview

1. A single-channel generative model is designed to reconstruct the phase channel and the amplitude channel remains unchanged, where a deep image prior and a total variation prior are encapsulated to realize convolutional smoothing and high-frequency information preservation.
2. The updated phase channel is held and a regularized optimization is introduced to update the amplitude channel, in which a Wirtinger gradient descent method based on total variation denoising is constructed to enable a good consistency of two channels.
3. As a result, the alternative iteration of these two tasks could stabilize convergence and realize edge-preserving wavefield reconstruction.

<div align=center><img src="/publications/imgs/DPENet/method.png" width=600></div>
<div align=center> Fig.1 Schematic illustration of DPENet. (a) Flowchart of DPENet. (b) Overview of UNet architecture. </div><br/>

# Experimental setup

<div align=center><img src="/publications/imgs/DPENet/Experimental_setup.png" width=550></div>

<div align=center> Fig.2 Experimental configuration. (a) Lensless transmitted setup. (b) Lensless reflective setup. </div><br/>

# Experimental results

<div align=center><img src="/publications/imgs/DPENet/r1.png" width=700></div>

<div align=center> Fig.3 Reconstructed resolution target with different methods. (a) Captured intensity pattern. (b)–(e) Retrieved by back-propagation, PhysenNet, CVUNet, and DPENet. </div><br/>

<div align=center><img src="/publications/imgs/DPENet/r2.png" width=700></div>

**Fig.4** Reconstructed phase images of label-free microglia cells with different methods. (a) Retrieved phase image by DPENet. (b) Ground truth phase image. (c)–(f) Retrieved and cropped from the red box by back-propagation, PhysenNet, CVUNet, and DPENet. (g) SSIM curve for different methods.

<div align=center><img src="/publications/imgs/DPENet/r3.png" width=450></div>

**Fig.5** Reconstructed phase images of label-free HeLa cells with different methods. (a) Retrieved phase image by DPENet. (b), (c) Histograms of CNR values in blue and orange boxes for different methods. (d1)–(d4), (e1)–(e4) Retrieved from blue and orange boxes by back-propagation, PhysenNet, CVUNet, and DPENet.

<div align=center><img src="/publications/imgs/DPENet/r4.png" width=500></div>

**Fig.6** Reconstructed results of reflective sample. (a) Captured intensity pattern. (b) Ground truth image retrieved by multi-distance phase retrieval. (c) SSIM curves. (d1)–(d3), (e1)–(e3), (f1)–(f3) Reconstructed by PhysenNet, CVUNet, and DPENet, respectively. (g) Histogram of SSIM values in selected iterations for different methods.

# Conclusion

In this work, we have proposed a dual-constrained untrained neural network for single-frame lensless imaging. In our method, the lensless imaging problem is remodeled into a phase-amplitude alternating optimization process. The phase updating problem is transformed into a regularized one with deep image and total variation priors. The sub-problem of amplitude updating is handled using a total variation denoising-based Wirtinger gradient descent method. The alternative iterative calculation of these two tasks could realize a high-quality and robust image reconstruction. Experiment results of resolution target, microglia cell, HeLa cell, SLM-based phase target, and pathological slide demonstrate that our method eliminates the twin-image artifact and accomplishes a high-fidelity single-frame phase recovery. 

In summary, our method provides an effective and robust way to solve the overfitting problem of untrained networks, which will facilitate further application of untrained networks in lensless imaging.


