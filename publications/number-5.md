---
layout: archive
title: "Lensfree auto-focusing imaging with coarse-to-fine tuning method"
---

### Published on: 06/02/2024 &emsp; in [*Optics and Lasers in Engineering*](https://www.sciencedirect.com/journal/optics-and-lasers-in-engineering)

In this work, we propose a coarse-to-fine tuning method to realize fast and robust lensfree auto-focusing imaging. In our method, a pre-defined simulation-driven focus network (sFocusNet) is constructed to find the coarse estimation of diffractive distances and output the searching range. Then, a new sharpness metric, regularization of gradient (RoG), is constructed with the combination of self-similarity prior and squared gradient map to get the final estimation within the searching range. With the obtained diffractive distances, a multi-height phase retrieval based on plug-and-play regularization is used for final image recovery. The experimental results on different samples are given to show the superiority of our method.

DOI: [10.1016/j.optlaseng.2024.108366](https://doi.org/10.1016/j.optlaseng.2024.108366)

[Supplemental document](../publications/materials/supp_for_sFocusNet.pdf)

Backward Links: [Publications](../_pages/publications.md) / [About Me](../_pages/about.md) / [Research](../_pages/research.md)

# Method Overview



# Experimental results



# Conclusion

In this paper, we have proposed a coarse-to-fine method, realizing fast and robust auto-focusing imaging for lensfree on-chip microscopes. 20 sets of samples are firstly used to prove that RoG metric outperforms other metrics with high robustness, accuracy, and unimodality. Then, the fast positioning of sFocusNet is proved and the running time of distance estimation can be decreased to ~4s for our method. Finally, new three commercial slides and a new CMOS sensor are used to conduct the extended experiment, which proves that our method shows better generalization than experiment-driven networks. We believe that our method will offer a practical auto-focusing solution for the commercialization of lensfree microscopes.
