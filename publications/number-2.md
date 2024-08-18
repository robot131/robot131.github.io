---
layout: archive
title: "Lensfree on-chip microscopy based on single-plane phase retrieval"
---

## Published in: 05/10/2022 &emsp; on [*Optics Express*](https://opg.optica.org/oe/home.cfm)

In this paper, we proposed a single-frame phase retrieval with nonlinear optimization, termed SFPR-NL, to realize high-fidelity sample reconstruction for lensfree on-chip microscopy. In our method, lensfree image recovery is constructed as a quadratic phase retrieval problem to reconstruct the transmitted field of the sample, where total variation and denoising priors are imposed to guarantee an efficient convergence. Based on the computational framework, we establish a 3D-printed lensless imaging platform to verify the superiority of our method.

DOI: [10.1364/OE.458400](https://doi.org/10.1364/OE.458400)

[Full text](../publications/materials/Single_PR.pdf) / [Supplemental document](../publications/materials/supp_for_Single_PR.pdf)

# Method Overview

<div align=center><img src="/publications/imgs/single/single-shot-method.png" width=700></div>

<div align=center> Fig.1 Diagram of lensfree on-chip microscope and flowchart of SFPR-NL algorithm. </div><br/>

# System design

<div align=center><img src="/publications/imgs/single/system.png" width=700></div>

Fig.2 Field-portable lensfree microscope used for experiment. (a) Optical configuration. (b) External view. (c) Internal view. (d) and (e) correspond to the experimental process for a slide-based sample and Petri dish. 

# Experimental results

<div align=center><img src="/publications/imgs/single/r1.png" width=700></div>

Fig. 3. Reconstructed results of positive resolution target (Ready Optics). SPR is the support-based phase retrieval. CS is the compressive sensing method. PhysenNet is the self-supervised learning method.

<div align=center><img src="/publications/imgs/single/r2.png" width=700></div>

<div align=center> Fig.3 Reconstructed phase images of label-free microglia cell (BV-2) </div><br/>

<div align=center><img src="/publications/imgs/single/r3.png" width=500></div>

Fig.4 Reconstructed results of polystyrene beads (50µm). (a1) and (a2) are recorded holograms when the sample is loaded or removed. (b1) and (b2) are reconstructed amplitude images that are related to the transmitted wave field and background field. (c) is obtained by subtracting the background field from the transmitted wave field. (d) is plotted from the blue cross-line of (c).

<div align=center><img src="/publications/imgs/single/r4.png" width=500></div>

Fig.5 Pixel super resolved reconstruction of the resolution target. (a-c) are reconstructed targets by using raw hologram, interpolated hologram, and pixel super-resolved hologram.

# Dynamic imaging results

<div align=center>
<video src="/publications/materials/single-1.mp4" autoplay="true" controls="controls" width="700">
</video>
</div>

<div align=center> Video.1 Video of phase reconstruction of living HeLa cell </div><br/>

<div align=center>
<video src="/publications/materials/single-2.mp4" autoplay="true" controls="controls" width="700">
</video>
</div>

<div align=center> Video.2 Video of reconstructed images of living eelworms </div><br/>

Backward Links: [Publications](../_pages/publications.md)
