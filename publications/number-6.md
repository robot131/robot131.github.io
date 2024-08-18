---
layout: archive
title: "Single-shot lensless masked imaging with enhanced self-calibrated phase retrieval"
---

## Published in: 07/10/2024 &emsp; on [*Optics Letters*](https://opg.optica.org/ol/home.cfm)

Single-shot lensless imaging with a binary amplitude mask enables a low-cost and miniaturized configuration for wave field recovery. However, the mask only allows a part of the wave field to be captured, and thus the inverse decoding process becomes a highly ill-posed problem. In our previous work [(SCPR)](../publications/number-3.md), we treated this as a wavefront completion problem, but it relies on time-lapse redundant data collection and its
dynamic imaging ability is constrained.

In this work we proposed an enhanced self-calibrated phase retrieval (eSCPR) method, realizing single-shot joint recovery of mask distribution and the sample’s wavefront. In our method, a sparse regularized phase retrieval (SrPR) algorithm is designed to calibrate the mask distribution. Then, a denoising regularized phase retrieval (DrPR) algorithm is constructed to reconstruct the wavefront of the sample. Compared to conventional single-shot methods, our method shows robust and flexible image recovery.

DOI: [10.1364/OL.528104](https://doi.org/10.1364/OL.528104)

[Supplemental document](../publications/materials/supp_for_eSCPR.pdf)

# Experimental Setup

The experimental setup of our single-shot LMI system is illustrated in Fig. 1(a). The process of light wave transmission can be summerized as following steps: 
1. A fiber laser with a wavelength of 532 nm is expanded by a collimated lens and then shaped by an aperture to generate plane wave illumination.
2. The incident wave loads on the sample, the transmitted wavefront of the sample is modulated by a binary amplitude mask
3. The intensity image is then recorded by a bare sensor chip (Sony, IMX206, pixel: 1.34 \\(\mu m\\) ), in which the sample-to-mask distance and the mask-to-sensor distance are denoted as \\(Z_1\\) and \\(Z_2\\), respectively.

<div align=center><img src="/publications/imgs/eSCPR_results/eSCPR_experimental.png" width=500></div>

<div align=center> Fig.1 Experimental Setup and the workflow of eSCPR. </div><br/>

The workflow of our method is given in Fig. 1(b). In Fig. 1(b1), the mask is closely installed on the sensor chip, and the diffraction pattern of the mask \\(I_M\\) is captured. Accordingly, the mask function can be retrieved by running the  sparse regularized phase retrieval (SrPR) with \\(I_M\\). Note that this mask calibration operation is **only done for once**. After that, the mask and the sensor could be integrated as **a coded camera** to reconstruct the sample’s wavefront. 

In Fig. 1(b2), the sample is loaded and the masked intensity image (\\(I_O\\)) is recorded. The wave field of the sample can be retrieved by running the denoising regularized phase retrieval (DrPR) with \\(I_O\\).

# Method Overview



<div align=center><img src="/publications/imgs/eSCPR_results/eSCPR_algor_1.png" width=400></div>

<div align=center> Fig.2 Workflow of the mask recovery step. </div><br/>

<div align=center><img src="/publications/imgs/eSCPR_results/eSCPR_algor_2.png" width=650></div>

<div align=center> Fig.3 Workflow of the mask-guided autofocusing step and the sample recovery step. </div><br/>

# Experimental Results

<div align=center><img src="/publications/imgs/eSCPR_results/r1.png" width=600></div>

**Fig.4** Reconstructed mask distribution functions by the SrPR under the mask’s pixel size of 5, 10, 20, and 40 µm. (a1)–(a4) are the recorded intensity images, where the auto-focusing curves of Z2 estimation are given in the subplots. (b1)–(b4) are the retrieved amplitude images of the masks.

<div align=center><img src="/publications/imgs/eSCPR_results/r2.png" width=600></div>

**Fig.5** Reconstructed resolution target by the DrPR algorithm under the mask’s pixel size of 5, 10, 20, and 40 µm. (a1)–(a4) are the captured masked intensity images, where the auto-focusing curves of Z1 estimation are given in the subplots. (b1)–(b4) are the retrieved amplitude images. (c1)–(c4) are expanded from green boxes in (b1)–(b4).

<div align=center><img src="/publications/imgs/eSCPR_results/r3.png"></div>

**Fig.6** Single-shot reconstructed results with different methods for maskless and masked imaging systems. (a1)–(e1) Maskless intensity images. (a2)–(e2) and (a3)–(e3) are retrieved with DPENet and SFPR-NL by running (a1)–(e1). (a4)–(e4) Masked intensity images. (a5)–(e5), (a6)–(e6), and (a7)–(e7) are retrieved with SPICA, SCPR, and our method by running (a4)–(e4). It should be emphasized that Figs. 4(a)–4(c) and Figs. 4(d)–4(e) exhibit the retrieved amplitude and phase images, respectively.

# Dynamic Imaging Results

<div align=center>
<video src="/publications/materials/eSCPR.mp4" autoplay="true" controls="controls" width="800">
</video>
</div>

<div align=center> Video.1 Video of raw dataset measurement and sample recovery of a dynamic Ronchi grating </div><br/>

# Conclusion

We proposed the eSCPR method to achieve joint recovery of mask distribution and sample’s wave field for single-shot LMI systems. In our design, the SrPR algorithm is constructed to retrieve the mask function, and then the sample-to-mask distance is estimated by mask-guided auto-focusing algorithm. Finally, the sample’s wavefront is recovered with the DrPR algorithm. Experimental results of different samples show the superiority of our method. We believe that our work will provide new technical support to design miniaturized wavefront sensors.

Backward Links: [Publications](../_pages/publications.md) / [About Me](../_pages/about.md) / [Research](../_pages/research.md)

