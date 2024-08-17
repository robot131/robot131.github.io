---
layout: archive
title: "Lensless masked imaging with self-calibrated phase retrieval"
---

## Published in: 06/12/2023 &emsp; on [*Optics Letters*](https://opg.optica.org/ol/home.cfm)

Lensless imaging with mask modulation is an attractive topic since it enables a compact configuration to acquire a complex wavefield of a sample with computational approaches. Most existing methods choose a customized phase mask for wavefront modulation and then decode the sample’s wave field from captured diffraction patterns. Different from phase masks, lensless imaging with a binary amplitude mask facilitates a cheaper fabrication cost, but the problem of high-quality mask calibration and image reconstruction have not been well resolved. In this paper, we proposed a self-calibrated phase retrieval (SCPR) method, realizing a joint recovery of a binary mask and sample’s wave field for a lensless masked imaging system. Compared with conventional methods, our method shows a high-performance and flexible image recovery.

DOI: [10.1364/OL.492476](https://doi.org/10.1364/OL.492476)

[Supplemental document](../publications/materials/supp_for_SCPR.pdf)

# Method Overview

The overview of lensless masked imaging is illustrated in Fig. 1. Figure 1(a) shows the experimental setup. In the system, a fiber-coupled laser emits coherent light for
illumination (wavelength: 532 nm). The incident wave lands on the sample and carries its information. The transmitted diffraction field from sample is sieved by a binary amplitude mask (pixel size = 4 $\mu m$) and the modulated intensity patterns are recorded by a CMOS sensor chip (IMX206, Sony, 4608 × 3456, pixel size is 1.34 $\mu m$), where the sample-to-mask distance is $Z_1$ and the mask-to-sensor distances are $Z_2^n, n \in [1,N]$ . The sensor is installed on a motorized stage (M-403, Physik Instrumente
Inc.) for multi-distance defocus measurement.

The SCPR method is composed of mask calibration and wave field recovery. As shown in Fig. 1(b), in mask calibration we use autofocusing method to acquire $Z_2^n$ and then reconstruct and calibrate the mask’s transmission function with $Z_2^n$ and the captured intensity images with/without the sample loaded, denoted as {$I_n^w, n \in [1,N]$} and {$I_n^{w/o}, n \in [1,N]$}, respectively. After that, we get the complex wave field of the aligned mask (M) and the mask-modulated sample at the sample plane ($U^w$). Then we feed the two complex wave fields in to the binary-coding phase retrieval algorithm, as shown in Fig. 1(c), and the complex wave field of sample can then be recovered. 

<img src="/publications/imgs/SCPR_method.png">

**Fig. 1.** Experimental setup of lensless masked imaging system and workflow of SCPR.

# Experimental Results


<div align=center><img src="/publications/imgs/SCPR_results/fig2.png" width=400></div>

<div align=center><img src="/publications/imgs/SCPR_results/fig3.png" width=700></div>

<div align=center><img src="/publications/imgs/SCPR_results/fig4.png" width=700></div>

<div align=center><img src="/publications/imgs/SCPR_results/fig5.png" width=700></div>

<div align=center><img src="/publications/imgs/SCPR_results/fig6.png" width=700></div>

<div align=center><img src="/publications/imgs/SCPR_results/fig7.png" width=500></div>







