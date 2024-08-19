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

The workflow of the DPENet is shown in Fig.1. It can be summarized as following steps:

1. A single-channel generative model is designed to reconstruct the phase channel and the amplitude channel remains unchanged.
2. A deep image prior and a total variation prior are encapsulated to realize convolutional smoothing and high-frequency information preservation.
3. The updated phase channel is held and a regularized optimization is introduced to update the amplitude channel, in which a Wirtinger gradient descent method based on total variation denoising is constructed to enable a good consistency of two channels.
4. As a result, the alternative iteration of these two tasks could stabilize convergence and realize edge-preserving wavefield reconstruction.

<div align=center><img src="/publications/imgs/DPENet/method.png" width=600></div>

<div align=center> Fig.1 Schematic illustration of DPENet. (a) Flowchart of DPENet. (b) Overview of UNet architecture. </div><br/>

# Experimental setup

Here we built two lensless systems for experimental validation, as shown in Fig. 2. The setup in Fig. 2(a) is used for imaging transmitted samples, and the process of light wave transmission can be summerized as following steps: 
1. A pinhole is mounted on the fiber laser (532 nm) to produce a spherical wave.
2. The wavefield is then transformed into plane wave illumination by a collimating lens.
3. The parallel beam travels through the sample and is recorded by a bare CMOS sensor chip (Sony, IMX206, 1.34 \\(\mu m\\) × 1.34 \\(\mu m\\)).

Another is to image the reflective samples, which is illustrated in Fig. 2(b), and the process of light wave transmission can be summerized as following steps: 
1. The plane wave is filtered by a polarizer, twisted by the beam splitter.
2. The wave then incident on a spatial light modulator (SLM, Holoeye GAEA-2-VIS- 036, 4160 × 2464, pixel pitch: 3.74 \\(\mu m\\)).
3. The light reflected from the SLM goes through the beam splitter and is captured by the sensor.

<div align=center><img src="/publications/imgs/DPENet/Experimental_setup.png" width=550></div>

<div align=center> Fig.2 Experimental configuration. (a) Lensless transmitted setup. (b) Lensless reflective setup. </div><br/>

# Experimental results

Four experimental results are shown here. The first one is amplitude-only object imaging, where a positive resolution target is used. The second one is to recover label-free microgila cells, while the third is HeLa cells. Finally, the experimental results of the reflective pure phase sample are illuminated.

### Resolution Target

The reconstructed resolution targets of PhysenNet, CVUNet, and DPENet are given in Fig.3. The results of resolution targets demonstrate that our method can realizehigh-fidelity image recovery for twin-image artifact elimination.

<div align=center><img src="/publications/imgs/DPENet/r1.png" width=700></div>

<div align=center> Fig.3 Reconstructed resolution target with different methods. (a) Captured intensity pattern. (b)–(e) Retrieved by back-propagation, PhysenNet, CVUNet, and DPENet. </div><br/>

### Label-Free Microgila Cells

The experimental results of label-free microglia cells are presented in Fig.4. Figure 4(a) shows the reconstructed phase image by our method, and the region of interest (ROI) is highlighted by the red box for a further visual comparison. The retrieved results of different methods are displayed in Figs.4(c)–(f).

It is noted that PhysenNet and CVUNet suffer from the overfitting problem and their SSIM curves remarkably vibrate. In contrast, the convergence curve of our method remains flattened and stable, which outputs high-fidelity image recovery.

<div align=center><img src="/publications/imgs/DPENet/r2.png" width=700></div>

**Fig.4** Reconstructed phase images of label-free microglia cells with different methods. (a) Retrieved phase image by DPENet. (b) Ground truth phase image. (c)–(f) Retrieved and cropped from the red box by back-propagation, PhysenNet, CVUNet, and DPENet. (g) SSIM curve for different methods.

### HeLa Cells

The reconstruction of HeLa cells is provided for further verification of phase imaging ability. The retrieved phase image from our method is shown in Fig.5(a). The retrieved regions from the blue and orange boxes are cropped and compared in Figs.5(d) and (e), in which blue and orange regions represent sparse and dense distribution, respectively. This result demonstrates that our method could achieve high-contrast phase imaging.

<div align=center><img src="/publications/imgs/DPENet/r3.png" width=450></div>

**Fig.5** Reconstructed phase images of label-free HeLa cells with different methods. (a) Retrieved phase image by DPENet. (b), (c) Histograms of CNR values in blue and orange boxes for different methods. (d1)–(d4), (e1)–(e4) Retrieved from blue and orange boxes by back-propagation, PhysenNet, CVUNet, and DPENet.

###  Reflective Pure Phase Sample

The experimental results of the reflective sample are presented in Fig.6. Figure 8(a) is the captured intensity pattern. With the multi-distance phase retrieval, the ground truth phase image is retrieved in Fig.6(b). The retrieved results of PhysenNet, CVUNet, and DPENet are given in Figs.6(d)–(f), where the corresponding SSIM curves are plotted in Fig.6(c).

It is noted that PhysenNet reaches its peak at 500 iterations and then drops remarkably. CVUNet slowly increases all through the iterations and shows bad convergence. DPENet meets its maximum and then keeps at a high and stable reconstruction accuracy. These results further prove the stable convergence of DPENet.

<div align=center><img src="/publications/imgs/DPENet/r4.png" width=500></div>

**Fig.6** Reconstructed results of reflective pure phase sample. (a) Captured intensity pattern. (b) Ground truth image retrieved by multi-distance phase retrieval. (c) SSIM curves. (d1)–(d3), (e1)–(e3), (f1)–(f3) Reconstructed by PhysenNet, CVUNet, and DPENet, respectively. (g) Histogram of SSIM values in selected iterations for different methods.

# Conclusion

In this work, we have proposed a dual-constrained untrained neural network for single-frame lensless imaging. In our method, the lensless imaging problem is remodeled into a phase-amplitude alternating optimization process. The phase updating problem is transformed into a regularized one with deep image and total variation priors. The sub-problem of amplitude updating is handled using a total variation denoising-based Wirtinger gradient descent method. The alternative iterative calculation of these two tasks could realize a high-quality and robust image reconstruction. Experiment results of resolution target, microglia cell, HeLa cell, SLM-based phase target, and pathological slide demonstrate that our method eliminates the twin-image artifact and accomplishes a high-fidelity single-frame phase recovery. 

In summary, our method provides an effective and robust way to solve the overfitting problem of untrained networks, which will facilitate further application of untrained networks in lensless imaging.


