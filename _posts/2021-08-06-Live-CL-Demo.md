---
title: "Typical (Neural-Network-Based) Classification vs. Zero-Shot, Part 3 - Live Demo of CL Toy"
description: See how "Triplet Loss" totally "crushes" the pairwise loss described in Part 1. 
layout: post
toc: false
comments: true
image: images/live-cl-demo.png
date: 2021-08-01 13:00:18
hide: false
search_exclude: false
typora-root-url: /Users/shawley
---

I added some more optional controls to the "[contrastive loss toy model](https://drscotthawley.github.io/blog/scottergories/2021/05/04/The-Joy-Of-3D.html#Contrastive-Loss-Cartoon-Demo)" from [Part I](https://drscotthawley.github.io/blog/scottergories/2021/05/04/The-Joy-Of-3D.html) that I want to demonstrate interactively, so this Part 3 post is in the form of a video:



<iframe width="560" height="315" src="https://www.youtube.com/embed/1cwc42sFA0A" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>



## Addenda:

### What I left out:

* Various ways of getting a handle on choosing negative examples and doing so in a computationally efficient way (e.g. via [Locality Sensitive Hashing](https://en.wikipedia.org/wiki/Locality-sensitive_hashing)).  But the paper by Wu et al has a good survey of these issues -- at least ca. 2017.  And since then you can find newer treatments of such things as well, and I encourage you to do so -- I'll be joining you.  Furthermore, if you follow the "Attract Only" methodology of SimCLR, then you wouldn't have any negative examples anyway. ;-) 
* Messing around with the toy model -- giving it "crazy" inputs like huge margins, whatever -- is not only fun (to me) but can also be quite informative as a process of "discovery": I'm sure I learned things in the contest of *experience* that I might otherwise have read (and maybe missed) in a paper. 



### What said that came off as maybe misleading:

(I'm new to this video-making thing and TBH not sure I ever want to get good at it. I realize I'm over-animated.)  

- I didn't mean to imply that CLIP used the "attract-only" scheme I attribute to SimCLR.  CLIP has a "contrastive loss" which means negative examples.  I was just talking about how the CLIP result on ImageNet demonstrated  the utility of metric-based, semi-supervised learning was demonstrated via 



## References

1. Jeremy Jordan's Twitter Page: https://twitter.com/jeremyjordan. Thanks Jeremy! 
2. **Wu, C.-Y.; Manmatha, R.; Smola, A.J.; Krähenbühl, P. [Sampling Matters in Deep Embedding Learning](https://openaccess.thecvf.com/content_ICCV_2017/papers/Wu_Sampling_Matters_in_ICCV_2017_paper.pdf). In Proceedings of the arXiv:1706.07567 [cs]; January 16 2018.**
3. "[CLIP](https://openai.com/blog/clip/)": Radford, A.; Kim, J.W.; Hallacy, C.; Ramesh, A.; Goh, G.; Agarwal, S.; Sastry, G.; Askell, A.; Mishkin, P.; Clark, J.; et al. [Learning Transferable Visual Models From Natural Language Supervision](https://arxiv.org/abs/2103.00020). ArXiv210300020 Cs 2021.  
4. Fonseca, E.; Ortego, D.; McGuinness, K.; O’Connor, N.E.; Serra, X. [Unsupervised Contrastive Learning of Sound Event Representations](https://arxiv.org/pdf/2011.07616.pdf). In Proceedings of the 2021 IEEE International Conference on Acoustics, Speech and Signal Processing (ICASSP); IEEE, 2021.
5. Hadsell, R.; Chopra, S.; LeCun, Y. [Dimensionality Reduction by Learning an Invariant Mapping](http://yann.lecun.com/exdb/publis/pdf/hadsell-chopra-lecun-06.pdf). In Proceedings of the 2006 IEEE Computer Society Conference on Computer Vision and Pattern Recognition (CVPR’06); 2006; Vol. 2, pp. 1735–1742.
6. "SimCLR": Chen, T.; Kornblith, S.; Norouzi, M.; Hinton, G. [A Simple Framework for Contrastive Learning of Visual Representations](https://arxiv.org/pdf/2002.05709.pdf). ArXiv200205709 Cs Stat 2020.
7. Alamar, J. "Illustrated Word2Vec", https://jalammar.github.io/illustrated-word2vec/
8. AK, "Gradio Demo for VQGAN+CLIP", *HuggingFace Spaces*, https://huggingface.co/spaces/akhaliq/VQGAN_CLIP