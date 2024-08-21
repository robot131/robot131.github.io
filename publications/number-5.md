---
layout: archive
title: "Lensfree auto-focusing imaging with coarse-to-fine tuning method"
---

### Published on: 06/02/2024 &emsp; in [*Optics and Lasers in Engineering*](https://www.sciencedirect.com/journal/optics-and-lasers-in-engineering)

In this work, we propose a coarse-to-fine tuning method to realize fast and robust lensfree auto-focusing imaging. In our method, a pre-defined simulation-driven focus network (sFocusNet) is constructed to find the coarse estimation of diffractive distances and output the searching range. Then, a new sharpness metric, regularization of gradient (RoG), is constructed with the combination of self-similarity prior and squared gradient map to get the final estimation within the searching range. With the obtained diffractive distances, a multi-height phase retrieval based on plug-and-play regularization is used for final image recovery. The experimental results on different samples are given to show the superiority of our method. 

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
2.  the obtained wavefield of the object \\((Ae^{iP})\\) is forward propagated by angular spectrum model with a set of diffractive distances to generate multi-distance intensity patterns \\(W_n\\)
3.  The intensity patterns (3000×3000×N ×13) are cropped into a mass of image patches \\(\overline{\omega_n}\\) with a size of 224×224 pixels.
4.  The small patches are transferred by fast Fourier transform into frequency-domain dataset and then labelled with the corresponding distances.
5.  The diffractive distances \\(z_n\\) and frequency-domain image sets \\(\omega_n\\) form the paired dataset.

The flowchart of network training is given in Fig. 3(b).  A cross-entropy loss function is used to mimic the difference between the input and output images.  An AdamW optimizer is applied to update the parameters of the network model.

<div align=center><img src="/publications/imgs/sFocusNet/data_generate.png" width=450></div>

<div align=center> Fig.3 The flowchart of dataset generation and network training. </div><br/>

## Regularization of gradient metric (RoG)

With the coarse range of the estimated distance, the next step is to propagate the recorded hologram to generate a Z-stack of back-propagated images and then construct a sharpness function to quantitatively assess the Z-stacked data so that an accurate diffractive distance can be obtained. Here, we combine the squared gradient map with the RED prior to form a regularization of gradient (RoG) metric for sharpness quantification. Based on the RoG metric, the detailed process of auto-focusing can be generalized as:

1. Assuming that the searching distance is \\(e_r, r \in [1,R] \\), the Z-stack of images are obtained by the back-propagation of the recorded holograms:

$$
\displaylines{
{S_r}{\rm{ = }}{{{\cal F}}^{ - 1}}\left[ {{{\cal F}}\left( {\sqrt {{I_m}} } \right) \odot H_r^*\left( {{e_r}} \right)} \right], r = 1,2,...,R,
}
$$

+ where \\(H_r^*\\) is a back-propagation frequency transfer function with the distance of \\(e_r\\) . \\(m\\) is the position index of multi-height measurement. 

2. The squared gradient maps of the Z-stack data are calculated as:

$$
\displaylines{
{G_r} = {\left| {\nabla \left( {{S_r}} \right)} \right|^2} = {\left| {{\nabla _x}\left( {{S_r}} \right)} \right|^2} + {\left| {{\nabla _y}\left( {{S_r}} \right)} \right|^2}}
$$ 

+ where \\({\nabla _x}\\) and \\({\nabla _y}\\) denote the gradient operators of \\(x\\) and \\(y\\) directions, respectively.

3. Calculating the RoG metric and taking its average through all pixels as the final value to assess the sharpness change, which is expressed as follows:

$$
\displaylines{
{\rm{RoG}}(r) = \frac{1}{{{N_x}{N_y}}}\sum\limits_{x = 1}^{{N_x}} {\sum\limits_{y = 1}^{{N_y}} {{{G_r}^T \left[ {{G_r} - {D_\sigma } \left( {{G_r}} \right)} \right]}}}.
}
$$ 

+ where \\(N_x\\) and \\(N_y\\) denote the pixel number along x and y directions. The flowchart of auto-focusing using RoG metric is illustrated in Fig.4.


<div align=center><img src="/publications/imgs/sFocusNet/ROG.png" width=700></div>

<div align=center> Fig.4 Flowchart of auto-focusing using Regularization of gradient metric (RoG). </div><br/>


# Experimental results

In experiment, we build a multi-height lensfree microscope to validate our method. In this system, a laser source with a wavelength of 532nm is expanded and collimated for plane wave illumination. Resolution target, homemade and commercial stained pathological slides, label-free cell, and random amplitude mask are orderly loaded as the samples for auto-focusing imaging. 

In data recording, the sample is closely held on a bare CMOS sensor chip (IMX206, pixel: 1.34 \\(\mu m\\), Sony) to form a near-field on-chip setup, where the sensor is installed on a motorized stage to capture multi-plane intensity images at five heights. The central regions with a size of 1000×1000 are cropped and used for auto-focusing imaging. 

In data processing, the captured images are firstly input into auto-focusing methods to acquire diffractive distances and then fed into the MDPR-PnP algorithm for image reconstruction.

## RoG validation

We prepare objective and subjective assessment criterions to judge the auto-focusing performance of the sharpness metrics.

+ Subjective assessment: We use all sharpness metrics to deal with intensity patterns to output a set of estimated distances, and then run the MDPR-PnP algorithm with the estimated distances for image reconstruction. By using visual discrimination on the retrieved images, we can find whether or not the real distances are accurately obtained by the metrics.
+ Objective assessment, we choose accuracy criterions, to further determine the auto-focusing performance of sharpness curves. The accuracy criterion of an auto-focusing sharpness curve is defined as:

$$
\displaylines{
{A_c} = \left| {{e_{ + \Delta }} - {e_{ - \Delta }}} \right|,
}
$$ 

### Resolution target

The auto-focusing results of resolution target (USAF 1951, Edmund) are shown in Fig.5. As the intensity pattern of the target is processed by all sharpness metrics, the auto-focusing curves are plotted in Fig. 6(a) and the selected curves captured from the orange region are enlarged in Fig.5(b).

As shown in Fig.5(a), three groups of distances can be estimated as follows: z=1.02mm (ToG, NoG, RoG), z=1.64mm (SPEC), and z=2mm (GRA, LAP, Tenengrad, SG). With the three distances, the amplitude images of resolution target are refocused by back-propagation in Figs.5(c-e). It is noted that only z=1.02mm outputs clear line pairs for resolution target, which means that ToG, NoG, and RoG metrics realize an accurate distance estimation.

<div align=center><img src="/publications/imgs/sFocusNet/r1.png" width=500></div>

**Fig.5** The auto-focusing results of resolution target. (a) Sharpness curves. (b) is zoomed-in curve from (a) and Ac values are labelled. (c–e) are the back-propagated results by using the estimated distance of 1.02mm, 1.64mm, and 2.00mm. 

### Pathological slide

The auto-focusing results of an H&E-stained pathological slide of testis of fish are offered in Fig.6. The sharpness curve of the intensity pattern at the first height is plotted in Fig.6(a) and its highlighted curve is zoomed in Fig.6(b). The multi-height distances of all metrics are estimated in Tab. 1, in which the distances are grouped into three kinds: Group I (SPEC), Group II (GRA, LAP, Tenengrad, SG), and Group III (ToG, NoG, RoG). With the above multi-height distances, the amplitude images of the slide are retrieved in Figs. 7(c-e). The corresponding highlighted regions are expanded in Figs. 7(f-h).

It is noted that the retrieved image in Fig. 7(f) is blurred and the tissue details cannot be distinguished, which means that the distances of Group I are not accurate. To further show the difference between Fig. 7(g) and Fig. 7(h), we crop the yellow regions with a size of 107μm×107μm and expand the regions in Fig. 7(i) and Fig. 7(j). As pointed out by the red arrows, the cell nucleus of Fig. 7(j) has a sharper morphology than that of Fig. 7(i). 

<div align=center><img src="/publications/imgs/sFocusNet/T1.png" width=500></div>

<div align=center> Table.1 The estimated distances by using different sharpness metrics for testis of fish. </div><br/>

<div align=center><img src="/publications/imgs/sFocusNet/r2.png" width=500></div>

**Fig.6** The auto-focusing results of testis of fish. (a) The sharpness curves of the captured intensity at the first height. (b) is the magnified curve from the red box in (a). (c–e) are reconstructed by the estimated distances of Group I, Group II, and Group III. (f–j) are expanded regions cropped from (c–e).

In addition to the above samples, we carry out 17 additional samples to compare the applicability of different metrics. The subjective assessment results of different metrics are listed in Tab. 2, where \\(‘\checkmark’\\) denotes successful distance estimation and \\(‘\XSolid’\\) means an unsuccessful auto-focusing result. The average running time of GRA, LAP, SPEC, Tenengrad, SG, ToG, NoG, and RoG is calculated as 23.2s, 36.9s, 20.9s, 24.2s, 24.1s, 34.5s, 49.8s, and 69.1s, in which the central region of 1000×1000 from multi-height patterns is cropped for time computation.

<div align=center><img src="/publications/imgs/sFocusNet/r3.png"></div>

<div align=center> Table.2 The auto-focusing performance summary of subjective assessment for 20 types of samples. </div><br/>

For objective assessment, the summarized results \\(A_C\\) are listed in Tab.3, respectively. It is noted that our RoG metric realizes the smallest values for both objective assessment results, which demonstrate the higher accuracy and better unimodality of our method.

<div align=center><img src="/publications/imgs/sFocusNet/r4.png"></div>

<div align=center> Table.3 The summary of accuracy criterion values (Ac) for 20 types of samples. </div><br/>

## sFocusNet validation



<div align=center><img src="/publications/imgs/sFocusNet/r5.png" width=750></div>

**Fig.7** Coarse distance estimation of 20 types of samples by using different frequency-domain simulation-driven networks. (a–e), (f–j), and (k–o) are focusing error plots with the training step size from 0.03mm to 0.07mm for SE-ResNet, MobileNetV3, and sFocusNet, respectively.

<div align=center><img src="/publications/imgs/sFocusNet/r6.png" width=450></div>

<div align=center> Table.4 Performance comparison of different simulation-driven networks for Fig.7. </div><br/>

<div align=center><img src="/publications/imgs/sFocusNet/r7.png"></div>

<div align=center> Table.5 The comparison of running time for different metrics. </div><br/>

## Validation on the network generalization

<div align=center><img src="/publications/imgs/sFocusNet/r8.png" width=700></div>

**Fig.8** The generalization validation of our method on new commercial pathological slides and new imaging sensor. (a) The used three commercial pathological slides. (b) is the focusing error plot of the new recorded experimental datasets for our sFocusNet. (c–e) are auto-focusing curves by using coarse-to-fine tuning. (f–h) are retrieved amplitude images of the three slides using the estimated distances from (c–e).

<div align=center><img src="/publications/imgs/sFocusNet/r9.png" width=750></div>

**Fig.9** The auto-focusing performance by using cross-validation for frequency-domain experiment-driven networks. (a–c) are focusing error plots of three networks when the paired datasets from one sample are used for training. (d–f) are focusing error plots of three networks when the paired datasets from two samples are used for training.

<div align=center><img src="/publications/imgs/sFocusNet/r10.png" width=450></div>

<div align=center> Table.6 Performance comparison of different experiment-driven networks for Fig.9. </div><br/>

# Conclusion

In this paper, we have proposed a coarse-to-fine method, realizing fast and robust auto-focusing imaging for lensfree on-chip microscopes. 20 sets of samples are firstly used to prove that RoG metric outperforms other metrics with high robustness, accuracy, and unimodality. Then, the fast positioning of sFocusNet is proved and the running time of distance estimation can be decreased to ~4s for our method. Finally, new three commercial slides and a new CMOS sensor are used to conduct the extended experiment, which proves that our method shows better generalization than experiment-driven networks. We believe that our method will offer a practical auto-focusing solution for the commercialization of lensfree microscopes.
