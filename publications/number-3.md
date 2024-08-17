---
title: "Lensless masked imaging with self-calibrated phase retrieval"
---

## Published in: 06/12/2023 &emsp; on [*Optics Letters*](https://opg.optica.org/ol/home.cfm)

Lensless imaging with mask modulation is an attractive topic since it enables a compact configuration to acquire a complex wavefield of a sample with computational approaches. Most existing methods choose a customized phase mask for wavefront modulation and then decode the sample’s wave field from captured diffraction patterns. Different from phase masks, lensless imaging with a binary amplitude mask facilitates a cheaper fabrication cost, but the problem of high-quality mask calibration and image reconstruction have not been well resolved. In this paper, we proposed a self-calibrated phase retrieval (SCPR) method, realizing a joint recovery of a binary mask and sample’s wave field for a lensless masked imaging system. Compared with conventional methods, our method shows a high-performance and flexible image recovery.

DOI: [10.1364/OL.492476](https://doi.org/10.1364/OL.492476)

[Supplemental document](../publications/materials/supp_for_SCPR.pdf)

# Method Overview

The overview of lensless masked imaging is illustrated in Fig. 1. Figure 1(a) shows the experimental setup. The process of light wave transmission can be summerized as following steps: 

1. A fiber-coupled laser emits coherent light for illumination (wavelength: 532 nm).
2. The incident wave lands on the sample and carries its information.
3. The transmitted diffraction field from sample is sieved by a binary amplitude mask (pixel size = 4 \\(\mu m\\))
4. The modulated intensity patterns are recorded by a CMOS sensor chip (IMX206, Sony, 4608 × 3456, pixel size is 1.34 \\(\mu m\\)).

The sample-to-mask distance is \\(Z_1\\) and the mask-to-sensor distances are \\(Z_2^n, n \in [1,N]\\) . The sensor is installed on a motorized stage (M-403, Physik Instrumente Inc.) for multi-distance defocus measurement.

The SCPR method is composed of mask calibration and wave field recovery. As shown in Fig. 1(b), in mask calibration we use autofocusing method to acquire \\(Z_2^n\\) and then reconstruct and calibrate the mask’s transmission function with \\(Z_2^n\\) and the captured intensity images with/without the sample loaded, denoted as { \\(I_n^w, n \in [1,N]\\) } and { \\(I_n^{w/o}, n \in [1,N]\\) }, respectively. After that, we get the complex wave field of the aligned mask (M) and the mask-modulated sample at the sample plane ( \\(U^w\\) ). Then we feed the two complex wave fields in to the binary-coding phase retrieval algorithm, as shown in Fig. 1(c), and the complex wave field of sample can then be recovered. 

<img src="/publications/imgs/SCPR_method.png">

**Fig. 1.** Experimental setup of lensless masked imaging system and workflow of SCPR.

# Experimental Results

To show the performance of our method, we first choose a resolution target as a sample. Fig. 2 shows the reconstruction results. Without the sample, 11 multi-distance intensity patterns \\(I_n^{w/o}\\) are captured by axially moving the motorized stage with a uniformly spaced interval. Then \\(I_n^{w/o}\\) are fed to the MDPR algorithm and \\(U^{w/o}\\) is reconstructed. Its amplitude image is shown in Fig. 2(a1).  As the resolution target is loaded, 11 modulated intensity patterns \\(I_n^x\\) are recordedand the corresponding amplitude image of \\(U^w\\) is retrieved, as shown in Fig. 2(a2). The pink and green regions of interest cropped from Fig. 2(a1) and Fig. 2(a2) are enlarged in Fig. 2(b1) and Fig. 2(b2). To explicitly show the lateral mismatch between \\(U^{w/o}\\) and \\(U^w\\), we synthesize Fig. 2(b1) and Fig. 2(b2) to produce a pseudo-color image in Fig. 2(c1), where pink is Fig. 2(b1), green is Fig. 2(b2), the overlapped region of them is white. After \\(U^{w/o}\\) is aligned to \\(U^w\\), the synthesized result using the aligned mask and \\(U^w\\) is displayed in Fig. 2(c2). It is noted that after alignment the two regions coincide with each other strictly, and the lateral mismatch error has been eliminated. Utlizing the mask before/after alignment, we reconstruct the resolution target, respectively, and Figs. 2(d1)–(d2) and Figs. 2(e1)–(e2) shows the corresponding results. It can be confirmed that the imaging resolution could be impaired without mask calibration.

<div align=center><img src="/publications/imgs/SCPR_results/fig2.png" width=400></div>


**Fig.2.** Reconstructed resolution target with/without mask calibration. (a1) and (a2) are retrieved amplitude images at the mask plane without/with sample loading, respectively. (b1) and (b2) are cropped regions from (a1) and (a2). (c1) is a synthesized pseudo-color figure to show the lateral mismatch between (b1) and (b2), in which pink is (b1), green is (b2), and the overlapped region of them is white. (c2) is a synthesized result after mask calibration. (d1)–(d2) and (e1)–(e2) are retrieved amplitude images of the resolution target without/with mask calibration, respectively. 

To further show the robustness of our method, we additionally choose three samples, including H&E-stained human tongue fungiform papillae, H&E-stained cow lung tissue, and pure phase target, to conduct image reconstruction experiments. The pure phase target is produced by a spatial light modulator (Holoeye GAEA-2-VIS-036, 4160×2464, pixel pitch: 3.74μm). Fig. 3. shows the autofocusing curves. The mask-to-sensor distances are acquired and plotted in Fig. 3(a), where the initial distance and interval are 
specified as 3.19mm and 0.10mm. For the three samples, their auto-focusing curves are plotted in Figs. 3 (b-d), where the sample-to-mask distances of human tongue fungiform papillae, cow lung tissue, and pure phase target are specified as 7.77mm, 8.73mm, and 58.29mm.

<div align=center><img src="/publications/imgs/SCPR_results/fig3.png" width=500></div>


**Fig.3.** The auto-focusing curves for additional experiments. (a) mask-to-sensor distance estimation. (b-d) are sample-to-mask distance estimation curves for human tongue fungiform papillae, cow lung tissue, and pure phase target.

With above parameters, the retrieved images of the three samples are given in Fig. 4, Fig. 5, and Fig. 6. The reconstructed results using 2 and 11 intensity patterns are displayed. The chosen three samples are also of three kind that can be classified as:

+ **Dense sample** (Fig. 4, human tongue fungiform papillae) : From the results shown in Fig. 4, we can see that when recovering dense biological tissue, our method shows a better imaging quality compared to the results of Multi-SPICA contaminated by noisy backgrounds.
+ **Sparse sample** (Fig. 5, lung tissue) : As shown in Fig. 5, it is noted that our method can reconstruct the lung tissue under dual-plane and multi-plane measurement, but Multi-SPICA only works well with multi-plane measurement.
+ **Phase only sample** (Fig. 6, pure phase target produced by a SLM) :  It is observed from Fig. 6 that both methods can reconstruct the pure phase image but our method shows a better imaging contrast.

<div align=center><img src="/publications/imgs/SCPR_results/fig4.png" width=600></div>

<div align=center> Fig.4. Reconstructed results of human tongue fungiform papillae for dual-plane and multi-plane measurement. </div><br/> 


<div align=center><img src="/publications/imgs/SCPR_results/fig5.png" width=600></div>

<div align=center> Fig.5. Reconstructed results of cow lung tissue for dual-plane and multi-plane measurement. </div><br/> 


<div align=center><img src="/publications/imgs/SCPR_results/fig6.png" width=600></div>

<div align=center> Fig.6. Reconstructed results of pure phase target for dual-plane and multi-plane measurement. </div><br/> 


We then use only one intensity image to reconstruct the complex field of the sample to test the single-shot reconstruction ability. The resolution target is chosen as the sample. The retrieved amplitude images of SPICA and our method are shown in Figs. 7(a1-a3) and Figs. 7(b1-b3). To further show the difference, the plotlines along green and red dash lines captured from Fig. 7(a3) and Fig. 7(b3) are pictured in Fig. 7(c1) and Fig. 7(c2). We can see that our method still outperforms the SPICA algorithm with a higher resolution and better imaging contrast.  However, compared to the results reconstruted with 11 intensity images, as shown in Fig. 2, there is a resolution loss.

<div align=center><img src="/publications/imgs/SCPR_results/fig7.png" width=450></div>

**Fig.7.** Single-shot reconstructed results of SPICA and binary-coding phase retrieval. (a1-a3) and (b1-b3) are reconstructed images of the SPICA algorithm and our method by using a single-frame intensity pattern. (c1-c2) are plotlines captured from (a3) and (b3).

# Conclusion and discussion

In summary, we proposed an lensless masked imaging method, termed SCPR, to jointly reconstruct the complex field of a sample and a binary amplitude mask. The experimental results of different samples have demonstrated that our method has a better imaging quality compared to conventional methods. Our work will provide an adaptive imaging modality to design a mask-based lensless microscope.





