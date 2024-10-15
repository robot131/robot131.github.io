---
layout: archive
title: "A portable lensfree imaging platform based on prior-guided phase retrieval"
---

### Under peer-review

In this paper, presented a portable lensfree imaging platform that can achieve complex wavefield reconstruction with multi-distance intensity measurements. In our platform, 400 LEGO bricks and a bare CMOS sensor chip are integrated into a lenslfree in-line holographic imaging system, where a motor and a set of gear modules from LEGO are designed to control the axial movement of a sample to generate multi-plane intensity patterns. 

In data processing, the intensity images are calculated in a computer to show the retrieved amplitude and phase of the sample. In addition, we propose a prior-guided phase retrieval algorithm (prGPR) to realize a data-efficient recovery, where only two intensity images are required to perform high-fidelity imaging performance. Experimental results of different kinds of samples are given to prove the effectiveness of our platform. We believe that our portable lensfree platform will provide a low-cost DIY microscope for hands-on science experiments.

Backward Links: [Publications](../_pages/publications.md) / [About Me](../_pages/about.md) / [Research](../_pages/research.md)

<span id="jump_top"></span>

## Abstract: 

+ [Experimental Setup](#jump1)
+ [Method Overview](#jump2)
  + [Prior-Guided Phase Retrieval](#jump2_1)
  + [Deep unfolding Atten-Unet](#jump2_2)
  + [Architecture of Atten-Unet](#jump2_3)
  + [Training details of the network](#jump2_4)
+ [Experimental Results](#jump3)
  + [Distance Estimation](#jump3_1)
  + [Multi-distance image reconstruction](#jump3_2)
  + [Effect of the Number of Input Intensity Patterns](#jump3_3)
  + [Dual-Plane and Single-Plane Image Reconstruction](#jump3_4)
  + [Running Time Discussion](#jump3_5)
  + [Ablation Study](#jump3_6)
  + [Cross-Validation](#jump3_7)
+ [Conclusion](#jump4)

# Experimental Setup <span id="jump1"></span>

The experimental setup is shown in Fig. 1(a). The 3D structure diagram of the portable lensfree imaging system is illustrated on the left side of Fig. 1(a), while the diagram of the optical setup is on the right side. Figs. 1(b-c) show the photographs of the platform. As shown in Fig. 1(a), the process of light wave transmission can be summerized as following steps:
1. A fiber-coupled laser is used as the light source to emit coherent light (wavelength: 532nm).
2. The light beam reaches the sample plane and loads its information.
3. A sample holder built of LEGO blocks and 3D-printed parts is designed to install the sample. The sample holder has been designed as a plug-in form for an easy sample switching.
4. The transmitted wavefield then propagates forward and its diffraction intensity patterns are captured by a CMOS image sensor chip (MT9J003, onsemi, 3840x2748, pixel size: 1.67 \\(\mu m\\) ).

<div align=center><img src="/publications/imgs/lego/fig1.png"></div>

<div align=center> Fig.1 Experimental setup of the portable lensfree imaging platform. </div><br/>

To get multi-plane intensity patterns, we set up a gear module on our platform to make the sample holder movable in the z-axis. As shown in Fig. 2(b), a pair of splines are installed on the back of the sample holder. The EV3 Medium Servo Motor (EV3, MINDSTORMS, Technical , 45503-1, LEGO), a motor of low load, high speed, and high accuracy, is utilized to provide energy and control the movement of the sample holder. As shown in Fig. 2(c1), combined with a worm gear reducer, we can convert the high-speed rotation of the motor into a slow one, realizing precise motion control. The profile perspective of the worm gear reducer is illustrated in Fig. 2(c2). To transmit the motion, we then build a gear train to connect the motor and the sample holder, as shown in Fig. 2(d1). Fig. 2(d2) gives the profile perspective.

<div align=center><img src="/publications/imgs/lego/fig2.png" width=500></div>

<div align=center> Fig.2 The transmission mechanism in our system. </div><br/>

[Back to the top](#jump_top)

# Method Overview <span id="jump2"></span>

As shown in Fig. 3, the image recovery is composed of two steps: auto-focusing and prior-guided phase retrieval (prGPR). In the auto-focusing, assuming the captured intensity patterns are denoted as \\({I_m},m \in [1,M]\\). The sample-to-sensor distances \\({Z_m},m \in [1,M]\\) can then be evaluated by utilizing the auto-focusing algorithm. With the above distances, the complex wavefield can be reconstructed by running the prGPR algorithm.

### Prior-Guided Phase Retrieval <span id="jump2_1"></span>

The workflow of prGPR is shown in Fig. 3(a). It can be summerized into four steps:
1. The initial guess of the mask's wavefiled at the mask plane is set as \\(O^{k}, k=0\\).
2. An alternative projection operation is conduct to replace the amplitude by the camera-captured intensity patterns \\({I_m},m \in [1,M]\\).
3. A pre-trained network is utlized as a pre-train prior generating a twin-image-free amplitude image. At the same time, a guide filter is utlized as a denoising prior to denoise the real and imaginary parts of the output wavefield respectively.
4. The guess of the modulated sample's wavefiled is update after a weighted feedback.

The iteration of the algorithm is \\(K\\). After \\(K\\) iteration, we can obtain the retrieved sample's wavefiled (\\(O^{K})\\).

<div align=center><img src="/publications/imgs/lego/fig.3.png" width=500></div>

<div align=center> Fig.3 The workflow of prior-guided phase retrieval. </div><br/>

[Back to the top](#jump_top)

### Deep unfolding Atten-Unet <span id="jump2_2"></span>

The architecture of the deep unfolding network is shown in Fig. 4(a). The input degraded image is first multiplied with the degradation matrix \\(C^T\\) to get an initial estimation \\(X^0\\). \\(X^0\\) is then fed into an Atten-Unet and parameterized by the matrix \\(\overline C\\) at the same time. The output of the Atten-Unet weighted by \\({\delta _1}{\eta _1}\\) is then added with \\(\overline C {X^0}\\) and \\({C^T}F\\) weighted by \\(\delta _1\\) to get the updated estimation \\(X^1\\).

The process repeated \\(N=3\\) times. Instead of fixing the value of the weight parameters, all the weight parameters in our network are set to be learnable through end-to-end training.

<div align=center><img src="/publications/imgs/lego/network.png" width=700></div>

<div align=center> Fig.4 The workflow of prior-guided phase retrieval. </div><br/>

### Architecture of Atten-Unet <span id="jump2_3"></span>

The Architecture of Atten-Unet \cite{oktay2018attention} is illustrated in Fig.4 (b). It consists of a contracting path (left side) and an expansive path (right side).

The structure of the attention block is shown in Fig. 4(c). The attention block is utilized to prevent dense predictions from small subsets of skip connections.

### Training details of the network <span id="jump2_4"></span>

The embedded Atten-Unet do not need to be pre-trained. Instead, the deep unfolding Atten-Unet (DUA-Unet), as illustrated in Fig. 4(a), is trained by supervised end-to-end training. Mean square error (MSE) is adopted as the loss function to train and update the parameters of DUA-Unet.

[Back to the top](#jump_top)

# Experimental Results <span id="jump3"></span>

### Distance Estimation <span id="jump3_1"></span>

Distance estimation is launched to calibrate the sample-to-sensor distances of the captured intensity patterns. The captured intensity patterns of the human goblet cells slide are shown in Fig 5(a). The distance estimation task can be regarded as an auto-focusing process. As shown in Fig. 5(b), we use the NoG metric to plot auto-focusing curves, where the sample-to-sensor distances \\({Z_m},m \in [1,M]\\) are specified as 2.91mm, 2.97mm, 3.07mm, 3.16mm, 3.34mm,	3.43mm,	3.64mm, 3.82mm, 4.01mm, 4.21mm and 4.42mm.

<div align=center><img src="/publications/imgs/lego/fig4.png" width=500></div>

**Fig.5.** The estimation of sample-to-sensor distances for the human goblet cells. (a) Intensity patterns of the human goblet cells. (b) Auto-focusing curves.

[Back to the top](#jump_top)

### Multi-distance image reconstruction <span id="jump3_2"></span>

We use 8 intensity patterns to recover the complex field of the sample to test the multi-distance image reconstruction capability of our method.  The experimental results of the human goblet cells are presented in Fig. 6.

The reference-free image quality assessment function  (ToG metric) is utilized to evaluate the quality of the recovery. The present multi-distance imaging methods, including APRDF, IWFR, SBMIR, and DPR-TV are chosen as the comparison group. For a fair comparison, we extend the dual-plane phase retrieval method DPR-TV into a multi-distance mode. The parameters of APRDF, IWFR, SBMIR, and DPR-TV methods are finely tuned.

<div align=center><img src="/publications/imgs/lego/multi-plane.png" width=500></div>

**Fig.6.** Reconstructed results of the human goblet cells. (a) Reconstructed image of our method. (b) Convergence curves. (c-g) Reconstructed images from red and blue boxes by using APRDF, IWFR, SBMIR, DPR-TV and our method.

[Back to the top](#jump_top)

### Effect of the Number of Input Intensity Patterns <span id="jump3_3"></span>

To analyze how the number of input intensity patterns influences the performance of our method, we change M from 1 to 10 and run our method for sample recovery. The corresponding results are given in Fig. 7. The retrieved image with 11 input intensity patterns is set as the ground truth image, as shown in Fig. 7(b). We use structural similarity index (SSIM) to compare the reconstructed accuracy. The SSIM values of the retrieved images with different numbers of input intensity patterns are plotted in Fig. 7(a). Figs. 7(c-g) show the reconstructed images with M=1,2,3,8,10.

<div align=center><img src="/publications/imgs/lego/multi-plane.png" width=500></div>

**Fig.7.** Reconstructed images of our method with different number of input intensity patterns. (a) SSIM values of images recovered with different number of input intensity patterns. (b) Ground truth image. (c-g) Images recovered with different number of input intensity patterns.

[Back to the top](#jump_top)

### Dual-Plane and Single-Plane Image Reconstruction <span id="jump3_4"></span>

Following the last subsection, we first run our method on the human goblet cells with M=1, 2. APRDF, IWFR, SBMIR, and DPR-TV algorithms are set as the comparison group with M=2, while pre-trained networks including Unet, Atten-Unet, deep-unfolding Unet (DU-Unet), and deep unfolding Atten-Unet (DUA-Unet) are used as the comparison group with M=1. The networks are all trained with the same dataset and parameter setting with the DUA-Unet utilized in our method. The reconstructed results are shown in Fig. 8. Fig. 8(a) is the SSIM histograms of the images reconstructed by different methods. Figs. 8(b1-b2) are the ground truth images of the selected two ROIs that are recovered with 8 intensity patterns by our method. Figs. 8(c-g) show the images reconstructed by different methods with M=2, while Figs. 8(h-l) show the results with M=1.

<div align=center><img src="/publications/imgs/lego/single-dual-compare.png" width=500></div>

**Fig.8.** Reconstructed images of the human goblet cells using single-plane or dual plane measurements. (a) SSIM Histograms of retrieved ROI images for different methods. (b) Ground truth images. (c-g) Reconstructed images of APRDF, IWFR, SBMIR, DPR-TV and our method with dual-plane intensity patterns. (h-l) Reconstructed images of Unet, Atten-Unet, DU-Unet, DUA-Unet and our method with single-plane intensity pattern.

As shown, our method retrieves the sample image with a clear background, high contrast, and sharp details (with M=2) compared to other methods. Unfortunately, as shown in Figs. 8(h-l), the single-plane retrieved results suffer from strong resolution loss. Thus, the number of input intensity patterns ($M$) is fixed at M=2 in the following experiments.  

The reconstructed images of different samples are shown in Fig. 9. Figs. 9(a1-e1) are the reconstructed amplitude images of a resolution target, while the ROI are outlined with the red box and magnified in the right bottom. Figs. 9(a2-e2) are retrieved amplitude images of an amplitude mask. Figs. 9(a3-e3) are recovered phase images of a label-free cells sample and the ROI are outlined with the yellow box and magnified in Figs. 9(a4-e4).

<div align=center><img src="/publications/imgs/lego/dual-plane.png" width=600></div>

**Fig.9.** Reconstructed images of different kinds of samples with dual-plane intensity patterns. (a-e) are retrieved by APRDF, IWFR, SBMIR, DPR-TV, and our method, respectively. It should be emphasized that (a1-e1), (a2-e2) and (a3-e3), (a4-e4) exhibit the retrieved amplitude and phase images, respectively.

[Back to the top](#jump_top)

### Running Time Discussion <span id="jump3_5"></span>

To compare the running time of our method with those of other methods, here we list the recorded running times in Table 1. Atten-UN, DU-UN, and DUA-UN denote Atten-Unet, deep-unfolding Unet (DU-Unet), and deep unfolding Atten-Unet (DUA-Unet), respectively. It should be emphasized that the times listed in Table 1 are the convergence times of the methods. When $M=8$, methods of the comparing group need 15 iterations. When $M=2$, they need 30 iterations. When $M=1$, the network methods just run for once. In contrast, our methods converges after only 7 iterations. The size of the input image is 1024x1024. Combine the previous results shown in Fig. 6, Fig. 8, and Fig. 9, we can say that our method achieves high-quality and time-saving reconstruction.

<div align=center><img src="/publications/imgs/lego/T1.png" width=400></div>

<div align=center> Table 1. Running time of different methods. </div><br/>

[Back to the top](#jump_top)

### Ablation Study<span id="jump3_6"></span>

We conducted an ablation study on a human goblet cells slide to evaluate the effectiveness of the priors in our method. Two intensity images are input to run the prGPR algorithm and the reconstructed images are shown in Fig. 10. The SSIM between the reconstructed image and the ground truth image are labeled under the corresponding images.

<div align=center><img src="/publications/imgs/lego/Ablation Study.png" width=500></div>

**Fig.10.** Ablation study of the priors in our method.  (a-c) Reconstructed images from red and blue boxes of our method with no prior, denoising prior and denoising prior + pre-trained prior. (d) Ground truth images.

[Back to the top](#jump_top)

### Cross-Validation <span id="jump3_7"></span>

We conducted a cross-validation to test the generalization performance of our DUA-Unet. This time we cut the training image pairs from 2 images of a stained human endometriosis slide and get the same number of image pairs as before. Then we embed the pre-trained network into our method and run on the breast tissue images that were used to train the network before. The results are illustrated in Fig. 10.

<div align=center><img src="/publications/imgs/lego/cross validation.png" width=400></div>

**Fig.11.** Cross-Validation.  (a-e) Reconstructed images of the selected two regions by APRDF, IWFR, SBMIR, DPR-TV and our method, respectively. The SSIM values are labeled under the crresponding images. (f) Ground truth images.

[Back to the top](#jump_top)

# Conclusion <span id="jump4"></span>

In summary, we designed a portable lensfree imaging platform with LEGO bricks and mechanical modules. A sample holder together with the motor and the gear module is designed to control the movement of the sample in the z-axis, the microscope has the ability to record multi-distance lensfree in-line holograms of specimens by a CMOS image sensor under coherent illumination. 

To reconstruct both the amplitude and the phase information of the sample with the intensity patterns, we have proposed a prior-guided phase retrieval algorithm. A denoising-prior-driven deep unfolding network is utilized as the pre-trained prior. Equipped with the denoising and pre-trained prior, our method realizes time-saving, high-quality image reconstruction compared to conventional methods. Experimental results of different kinds of samples have demonstrated the superiority of our method. 

Built of blocks, our design provides a low-cost lensfree microscope for initiation science education, giving more children a chance to launch hands-on science experiments.

[Back to the top](#jump_top)

Backward Links: [Publications](../_pages/publications.md) / [About Me](../_pages/about.md) / [Research](../_pages/research.md)
