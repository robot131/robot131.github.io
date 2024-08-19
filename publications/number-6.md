---
layout: archive
title: "Single-shot lensless masked imaging with enhanced self-calibrated phase retrieval"
---

### Published on: 07/10/2024 &emsp; in [*Optics Letters*](https://opg.optica.org/ol/home.cfm)

Single-shot lensless imaging with a binary amplitude mask enables a low-cost and miniaturized configuration for wave field recovery. However, the mask only allows a part of the wave field to be captured, and thus the inverse decoding process becomes a highly ill-posed problem. In our previous work [(SCPR)](../publications/number-3.md), we treated this as a wavefront completion problem, but it relies on time-lapse redundant data collection and its
dynamic imaging ability is constrained.

In this work we proposed an enhanced self-calibrated phase retrieval (eSCPR) method, introducing the idea of wavefront decoupling into LMI systems, which was commonly used in ptychographic iterative engine (PIE) imaging systems and realizing single-shot joint recovery of mask distribution and the sample’s wavefront. 

In our method, a sparse regularized phase retrieval (SrPR) algorithm is designed to calibrate the mask distribution. Then, a denoising regularized phase retrieval (DrPR) algorithm is constructed to reconstruct the wavefront of the sample. Compared to conventional single-shot methods, our method shows robust and flexible image recovery.

DOI: [10.1364/OL.528104](https://doi.org/10.1364/OL.528104)

[Supplemental document](../publications/materials/supp_for_eSCPR.pdf)

Backward Links: [Publications](../_pages/publications.md) / [About Me](../_pages/about.md) / [Research](../_pages/research.md)

<span id="jump_top"></span>

## Abstract: 

+ [Experimental Setup](#jump1)
+ [Method Overview](#jump2)
  + [Mask Recovery](#jump2_1)
  + [Mask-Guided Auto-Focusing](#jump2_2)
  + [Sample Recovery](#jump2_3)
+ [Experimental Results](#jump3)
  + [Mask Recovery](#jump3_1)
  + [Resolution Target](#jump3_2)
  + [Reconstructed Results of Various Kinds of Samples](#jump3_3)
  + [Dynamic Imaging Results](#jump3_4)
+ [Conclusion](#jump4)

# Experimental Setup <span id="jump1"></span>

The experimental setup of our single-shot LMI system is illustrated in Fig. 1(a). The process of light wave transmission can be summerized as following steps: 
1. A fiber laser with a wavelength of 532 nm is expanded by a collimated lens and then shaped by an aperture to generate plane wave illumination.
2. The incident wave loads on the sample, the transmitted wavefront of the sample is modulated by a binary amplitude mask
3. The intensity image is then recorded by a bare sensor chip (Sony, IMX206, pixel: 1.34 \\(\mu m\\) )
The sample-to-mask distance and the mask-to-sensor distance are denoted as \\(Z_1\\) and \\(Z_2\\), respectively.

<div align=center><img src="/publications/imgs/eSCPR_results/eSCPR_experimental_setup.png" width=550></div>

<div align=center> Fig.1 Experimental Setup and the workflow of eSCPR. </div><br/>

The workflow of our method is given in Fig. 1(b). In Fig. 1(b1), the mask is closely installed on the sensor chip, and the diffraction pattern of the mask \\((I_M)\\) is captured. Accordingly, the mask function can be retrieved by running the  sparse regularized phase retrieval (SrPR) with \\(I_M\\). Note that this mask calibration operation is **only done for once**. After that, the mask and the sensor could be integrated as **a coded camera** to reconstruct the sample’s wavefront. In Fig. 1(b2), the sample is loaded and the masked intensity image \\((I_O)\\) is recorded. The wave field of the sample can be retrieved by running the denoising regularized phase retrieval (DrPR) with \\(I_O\\).

[Back to the top](#jump_top)

# Method Overview <span id="jump2"></span>

The eSCPR method is composed of mask recovery, mask-guided auto-focusing and sample recovery. In a LMI systems, a known mask distribution is a constraint. So we first retrieve the mask in the mask recovery step. Since the sample's wavefiled is modulated by the mask, the diffraction distance between the mask and the sample becomes hard to calibrate by conventional auto-focusing method. In this case, we designed a mask-guided auto-focusing to estimate the sample-to-mask distance \\((Z_1)\\). Finally, with the retrieved mask, the sample-to-mask distance \\((Z_1)\\), the mask-to-sensor distance \\((Z_2)\\) and the masked intensity image \\((I_O)\\), we could recover the complex wavefield of the sample in the sample recovery step. Details are described in the following sections. Detailed derivations are presented in the [Supplemental document](../publications/materials/supp_for_eSCPR.pdf).

### Mask Recovery <span id="jump2_1"></span>
The workflow of the mask recovery step is shown in Fig.2. We first retrieve the wavefield of the mask with single-frame measurement \\((I_M)\\). construct SrPR algorithm to solve the optimization problem marked on the top of Fig.2. The algorithm is derivated with the use of PnP-FISTA solver. The process of this step can be summarized as follows:

1. The initial guess of the mask's wavefiled at the mask plane is set as \\(M^{k_1}, k_1=0\\).
2. The amplitude of the output wavefield is replace by the camera-captured one \\((\sqrt{I_M})\\) in the alternative projection operation.
3. The wavefiled is then constrained by a sparse regularization operation. 
4. A pre-trained network, [TNRD](https://doi.org/10.1109/tpami.2016.2596743), is utlized as the denoiser to denoise the real and imaginary part of the output wavefield respectively.
5. The guess of the modulated sample's wavefiled is update after a weighted feedback.

The iteration of the algorithm is \\(K_1\\). After \\(K_1\\) iteration, we can obtain the retrieved sample's wavefiled (\\(M^{K_1})\\).

<div align=center><img src="/publications/imgs/eSCPR_results/eSCPR_algor_1.png" width=450></div>

<div align=center> Fig.2 Workflow of the mask recovery step. </div><br/>

[Back to the top](#jump_top)

### Mask-Guided Auto-Focusing <span id="jump2_2"></span>

The workflow of the mask-guided auto-focusing step is shown in Fig.3. Since the sample's wavefiled is modulated by the mask and cannot be obtained by conventional auto-focusing method, we designed a mask-guided auto-focusing to estimate the sample-to-mask distance \\((Z_1)\\). The algorithm is derivated with the use of PnP-FISTA solver. We first retrieve the modulated sample's wavefiled at the mask plane. The process of this step can be summarized as follows:

1. The initial guess of the modulated sample's wavefiled at the mask plane is set as \\(C^{k_2}, k_2=0\\).
2. The amplitude of the output wavefield is replace by the camera-captured one \\((\sqrt{I_O})\\) in the alternative projection operation.
3. A wavefield decoupling operation is conducted to decouple the sample's wavefield from the modulated one, while the recoverd mask \\((M)\\) is seen as the illmination function.
4. The [guided filter](https://doi.org/10.1007/978-3-642-15549-9_1) is utlized as the denoiser to denoise the real and imaginary part of the wavefield respectively.
5. The guess of the modulated sample's wavefiled is update after a weighted feedback.

The iteration is set \\(K_2\\). After \\(K_2\\) iteration, the modulated sample's wavefiled at the mask plane is obtained. We then use ToG metric to draw the auto-focusing curve and the sample-to-mask distance \\((Z_1)\\) can be estimate.

<div align=center><img src="/publications/imgs/eSCPR_results/eSCPR_algor_2.png" width=750></div>

<div align=center> Fig.3 Workflow of the mask-guided autofocusing step. </div><br/>

[Back to the top](#jump_top)

### Sample Recovery <span id="jump2_3"></span>

After the mask function is retrieved, i.e.,(\\(M=M^{K_1}\\)), and the sample-to-mask distance \\((Z_1)\\) is obtained, we then construct DrPR algorithm to retrieve the wavefield of sample by processing the masked intensity image (\\(I_O)\\). Different from [SCPR](../publications/number-3.md), the retrieved mask here is treated as a illmination function and does not need to be binarized for sample recovery. The workflow of the sample recovery step is shown in Fig.4, while the constructed optimization problem is marked on the top. The algorithm is derivated with the use of PnP-FISTA solver. The process of this step can be summarized as follows:

1. The initial guess of the sample's wavefiled is set as \\(O^{k_3}, k_3=0\\).
2. The \\((O^{k_3})\\) is diffracted to the mask plane and modulated by the mask, output as \\(M \odot (A_{Z_1} O^{k_3})\\). \\(A_Z\\) is the diffraction operator with the diffraction distance \\(Z\\).
3. The amplitude of the output wavefield is replace by the camera-captured one \\((\sqrt{I_O})\\) in the alternative projection operation.
4. A wavefield decoupling operation is conducted to decouple the sample's wavefield from the modulated one, while the recoverd mask \\((M)\\) is seen as the illmination function.
5. The decoupled wavefield is inverse diffracted to the sample plane. A pre-trained network, [TNRD](https://doi.org/10.1109/tpami.2016.2596743), is utlized as the denoiser to denoise the real and imaginary part of the wavefield respectively.
6. The guess of the sample's wavefiled is update after a weighted feedback.

The iteration of the algorithm is \\(K_3\\). After \\(K_3\\) iteration, we can obtain the retrieved sample's wavefiled (\\(O^{K_3})\\).

<div align=center><img src="/publications/imgs/eSCPR_results/eSCPR_algor_3.png" width=750></div>

<div align=center> Fig.4 Workflow of the sample recovery step. </div><br/>

[Back to the top](#jump_top)

# Experimental Results <span id="jump3"></span>

### Mask Recovery <span id="jump3_1"></span>

We fabricate five binary amplitudemasks with pixel sizes of 2.5, 5, 10, 20, and 40 \\(\mu m\\) to test the performance of the SrPR, in which the mask is installed on the sensor chip to record the intensity image. The recorded intensity images of different masks are shown in Figs.5(a1)–(a4) and the auto-focusing curves of \\(Z_2\\) are plotted in the subplots. The amplitude images of the mask retrieved by the SrPR are shown in Figs. 5(b1)–(b4). The regions of 134 \\(\mu m\\) × 134 \\(\mu m\\) are expanded as the subplots. In Fig.5, the SrPR finishes single-frame recovery of the masks with the pixel size from 5 to 40 µm. But the retrieval with a mask pixel of 2.5 \\(\mu m\\) is unsuccessful

<div align=center><img src="/publications/imgs/eSCPR_results/r1.png" width=600></div>

**Fig.5** Reconstructed mask distribution functions by the SrPR under the mask’s pixel size of 5, 10, 20, and 40 µm. (a1)–(a4) are the recorded intensity images, where the auto-focusing curves of Z2 estimation are given in the subplots. (b1)–(b4) are the retrieved amplitude images of the masks.

[Back to the top](#jump_top)

### Resolution Target <span id="jump3_2"></span>

A resolution target (Thorlabs) is then loaded as the sample. The masked intensity images are shown in Figs.5(a1)-(a4). By using mask-guided auto-focusing, the auto-focusing curves of \\(Z_1\\) are plotted in the subsets of Figs.6(a1)–(a4) and \\(Z_1\\) can be acquired. The amplitude images of the sample recovered by DrPR are illuminated in Figs.6(b1)–(b4), and the green regions are zoomed in Figs.5(c1)–(c4)

It is noted that DrPR achieves single-frame recovery but the performance on the mask’s pixel sizes is different. In Figs.6(c1)–(c4), a smaller mask pixel contributes a better imaging quality and the results with large mask pixels are undermined by messy backgrounds.

<div align=center><img src="/publications/imgs/eSCPR_results/r2.png" width=600></div>

**Fig.6** Reconstructed resolution target by the DrPR algorithm under the mask’s pixel size of 5, 10, 20, and 40 µm. (a1)–(a4) are the captured masked intensity images, where the auto-focusing curves of Z1 estimation are given in the subplots. (b1)–(b4) are the retrieved amplitude images. (c1)–(c4) are expanded from green boxes in (b1)–(b4).

[Back to the top](#jump_top)

### Reconstructed Results of Various Kinds of Samples <span id="jump3_3"></span>

In the following experiments, we use the mask with the pixel of 5 \\(\mu m\\) for wavefront modulation and select five samples to further validate our method, including high-resolution target (55-622, Edmund), Ronchi grating (R1L3S13N, Thorlabs), stained pathological slide (Human Tongue Fungiform Papillae), binary random phase mask (pixel:10 \\(\mu m\\)), and reflective phase-only target produced from a spatial light modulator (SLM, Holoeye, GAEA-2-VIS-036). Herebtwo maskless phase retrieval methods (DPENet and SFPR-NL) and two masked phase retrieval methods (SPICA and SCPR) are listed for the comparison group. The results are shown in Fig.7.

<div align=center><img src="/publications/imgs/eSCPR_results/r3.png"></div>

**Fig.7** Single-shot reconstructed results with different methods for maskless and masked imaging systems. (a1)–(e1) Maskless intensity images. (a2)–(e2) and (a3)–(e3) are retrieved with DPENet and SFPR-NL by running (a1)–(e1). (a4)–(e4) Masked intensity images. (a5)–(e5), (a6)–(e6), and (a7)–(e7) are retrieved with SPICA, SCPR, and our method by running (a4)–(e4). It should be emphasized that Figs. 4(a)–4(c) and Figs. 4(d)–4(e) exhibit the retrieved amplitude and phase images, respectively.

The results in Fig.7 demonstrate that our method outperforms other methods with high-performance recovery. Compared to maskless phase retrieval, our method introduces a mask as a strong physical constraint, which effectively mitigates the stagnant problem of single-frame wavefront recovery. Moreover, the wave field decoupling of the mask function could extract the messy background, and thus the retrieved phase image of our method shows an enhanced imaging quality.

[Back to the top](#jump_top)

### Dynamic Imaging Results <span id="jump3_4"></span>

The experimental configuration and reconstructed results of the dynamic imaging experiment are shown in Fig.8. We install the Rongchi grating on a motorized rotation stage (PRM1/MZ8, Thorlabs) and then use this rotating grating as a moving target for observation. As shown in Fig.8(a), the diffraction patterns of the rotating sample are modulated by the binary amplitude mask, and the masked intensity images are captured by the sensor chip. 

In data recording, the grating is rotated with 50 degrees in about 5 seconds, and a total of 50 masked intensity images are recorded. The mask-to-sensor distance (\\(Z_2\\)) is calibrated as 2.37mm. Considering that the grating may be installed with a tilt angle, we perform the mask-guided auto-focusing algorithm to get the sample-to-mask distance (\\(Z_1\\)) for each masked intensity image. 

With the above parameters, we feed the masked intensity images into DrPR algorithm to reconstruct the rotating target. The recorded masked intensity images at the time of 0.5s, 1.2s, and 2.6s are presented in Figs.8(b1-b3), and the retrieved amplitude images of the rating are shown in Figs.8(c1-c3). It is noted that our method can accomplish the dynamic imaging of the rotating target, proving the dynamic imaging capability of our method.

<div align=center><img src="/publications/imgs/eSCPR_results/dynamic.png" width="600"></div>

**Fig.8** Experimental results of dynamic imaging using our single-shot lensless masked imaging system. (a) Experimental configuration. (b1-b3) are the masked intensity images recorded at the time of 0.5s, 1.2s, and 2.6s. (c1-c3) are reconstructed amplitude images of the grating by running DrPR algorithm with (b1-b3).

The following video shows the entire process of raw dataset measurement and sample recovery.

<div align=center>
<video src="/publications/materials/eSCPR.mp4" autoplay="true" controls="controls" width="800">
</video>
</div>

**Video.1** Video of raw dataset measurement and sample recovery results of the dynamic Ronchi grating sample in Fig.7

[Back to the top](#jump_top)

# Conclusion <span id="jump4"></span>

We proposed the eSCPR method to achieve joint recovery of mask distribution and sample’s wave field for single-shot LMI systems. In our design, the SrPR algorithm is constructed to retrieve the mask function, and then the sample-to-mask distance is estimated by mask-guided auto-focusing algorithm. Finally, the sample’s wavefront is recovered with the DrPR algorithm. Experimental results of different samples show the superiority of our method. We believe that our work will provide new technical support to design miniaturized wavefront sensors.

[Back to the top](#jump_top)

Backward Links: [Publications](../_pages/publications.md) / [About Me](../_pages/about.md) / [Research](../_pages/research.md)

