---
title: "Typical (Neural-Network-Based) Classification vs. Zero-Shot, Part 3 - Live Demo on CL Toy"
description: See how Triple Loss totally "crushes" the pairwise loss described in Part 1. 
layout: post
toc: false
comments: true
image: images/live-cl-demo.png
date: 2021-08-01 13:00:18
hide: false
search_exclude: false
typora-root-url: /Users/shawley
---

I added some more optional controls to the "contrastive loss toy model" from [Part I](https://drscotthawley.github.io/blog/scottergories/2021/05/04/The-Joy-Of-3D.html) that I want to demonstrate interactively, so this Part 3 post is in the form of a video:



<iframe width="560" height="315" src="https://www.youtube.com/embed/1cwc42sFA0A" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>



## NB: What I left out! 

What I forgot to talk about in the video were various ways of getting a handle on choosing negative examples and doing so in a computationally efficient way (e.g. via Locality Sensitive Hashing).  But the paper by Wu et al has a good survey of these issues -- at least ca. 2017.  But one can find newer treatments of such things as well, and I encourage you to do so -- I'll be joining you.  Furthermore, if you follow the "Attract Only" methodology of SimCLR, then you wouldn't have any negative examples anyway. ;-) 



## References

1. Wu, C.-Y.; Manmatha, R.; Smola, A.J.; Krähenbühl, P. Sampling Matters in Deep Embedding Learning. In Proceedings of the arXiv:1706.07567 [cs]; January 16 2018.
2. "CLIP": Radford, A.; Kim, J.W.; Hallacy, C.; Ramesh, A.; Goh, G.; Agarwal, S.; Sastry, G.; Askell, A.; Mishkin, P.; Clark, J.; et al. Learning Transferable Visual Models From Natural Language Supervision. ArXiv210300020 Cs 2021.  
3. Fonseca, E.; Ortego, D.; McGuinness, K.; O’Connor, N.E.; Serra, X. Unsupervised Contrastive Learning of Sound Event Representations. In Proceedings of the 2021 IEEE International Conference on Acoustics, Speech and Signal Processing (ICASSP); IEEE, 2021.
4. Hadsell, R.; Chopra, S.; LeCun, Y. Dimensionality Reduction by Learning an Invariant Mapping. In Proceedings of the 2006 IEEE Computer Society Conference on Computer Vision and Pattern Recognition (CVPR’06); 2006; Vol. 2, pp. 1735–1742.
5. "SimCLR": Chen, T.; Kornblith, S.; Norouzi, M.; Hinton, G. A Simple Framework for Contrastive Learning of Visual Representations. ArXiv200205709 Cs Stat 2020.
6. Alamar, J. "Illustrated Word2Vec", https://jalammar.github.io/illustrated-word2vec/
7. AK, "Gradio Demo for VQGAN+CLIP", *HuggingFace Spaces*, https://huggingface.co/spaces/akhaliq/VQGAN_CLIP