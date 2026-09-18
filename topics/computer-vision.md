# Computer Vision

Part of [An Always*-Updating List of LLM/Language/Vision Resources](../README.md).

Two threads run through this file and they are largely independent.

The **generative** thread is the one people usually want: VAEs, then GANs, then diffusion, then the 2023 scramble to personalize text-to-image models cheaply. It is presented roughly in the order the field discovered things, because diffusion genuinely does not make sense until you have seen a VAE, and the VQ half of modern image tokenizers comes straight out of the GAN era.

The **recognition** thread is AlexNet through ViT and CLIP, then vision-language models, then video. If you already did computer vision before 2020 you can skip most of it.

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [The Generative Thread](#the-generative-thread)
  - [VAEs and Variational Inference](#vaes-and-variational-inference)
  - [GANs](#gans)
  - [From VAEs to Diffusion](#from-vaes-to-diffusion)
  - [Diffusion Models](#diffusion-models)
  - [Text-to-Image Personalization](#text-to-image-personalization)
- [The Recognition Thread](#the-recognition-thread)
  - [Pre-Diffusion Classics](#pre-diffusion-classics)
  - [Vision-Language Models (VLMs)](#vision-language-models-vlms)
  - [Video Understanding Models](#video-understanding-models)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

---

# The Generative Thread

## VAEs and Variational Inference

The autoencoder is obvious. The *variational* part is where people lose the thread, and it is worth not losing, because the ELBO shows up again in diffusion and the encoder-decoder pair shows up again as the thing Stable Diffusion runs inside.

- [From Autoencoder to Beta-VAE](https://lilianweng.github.io/posts/2018-08-12-vae/) - start here. Walks autoencoder to denoising to sparse to VAE to beta-VAE to VQ-VAE, and that last step feeds directly into VQGAN below
- [Auto-Encoding Variational Bayes](https://arxiv.org/abs/1312.6114) - Kingma and Welling, the original
- [An Introduction to Variational Autoencoders](https://arxiv.org/abs/1906.02691) - the same authors explaining their own work at monograph length six years later, and a gentler rung than the paper
- [Variational Auto-Encoders and the Expectation-Maximization Algorithm](https://maurocamaraescudero.netlify.app/post/variational-auto-encoders-and-the-expectation-maximization-algorithm/) - the connection to EM, which most tutorials skip entirely

Two questions everyone has partway through the derivation, answered properly:

- [Why do we start from KL(q(z)||p(z|x)) in the ELBO derivation?](https://stats.stackexchange.com/questions/531503/why-do-we-start-from-kldqz-pzx-in-elbo-derivation)
- [Why does maximizing the lower bound maximize the probability?](https://stats.stackexchange.com/questions/315841/why-maximizing-the-lower-bound-of-variational-evidence-maximizes-the-probability)

## GANs

Nobody trains GANs anymore. Read this section anyway: adversarial training is where the field learned what unstable optimization feels like, mode collapse is still the canonical failure mode for any generative objective, and VQGAN is the direct ancestor of every image tokenizer in use today.

- [How to Train a GAN (ganhacks)](https://github.com/soumith/ganhacks) - a list of superstitions from NIPS 2016, and the best surviving artifact of what training these things was actually like
- [Image-to-Image Translation with Conditional Adversarial Networks](https://arxiv.org/abs/1611.07004) - pix2pix. Conditional generation is the idea that survived, more or less intact, into ControlNet
- [Taming Transformers for High-Resolution Image Synthesis](https://arxiv.org/abs/2012.09841) - VQGAN. Discrete latents plus a transformer prior, which is the recipe the current generation of image and video tokenizers still runs
- [The Illustrated VQGAN](https://ljvmiranda921.github.io/notebook/2021/08/08/clip-vqgan/) - the readable version of the above, with the CLIP-guided variant that briefly ate the internet in 2021
- [Limitations of Encoder-Decoder GAN architectures](http://www.offconvex.org/2018/03/12/bigan/) - Arora on why BiGAN cannot learn the representations it was claimed to. Theory, so it has not aged

## From VAEs to Diffusion

- [Diffusion Models as a kind of VAE](https://angusturner.github.io/generative_models/2021/06/29/diffusion-probabilistic-models-I.html) - the bridge. If the previous section landed, this reframes DDPM as a hierarchical VAE with a fixed encoder and the whole thing clicks
- [How AI Image Generators Work (Computerphile)](https://www.youtube.com/watch?v=1CIpzeNxIhU) - fifteen minutes, no maths, and correct. Good to send to people who do not want any of the above

## Diffusion Models

- [Lilian Weng's "What are Diffusion Models?"](https://lilianweng.github.io/posts/2021-07-11-diffusion-models/) - still the best first read on DDPMs, score based models and NCSN
- [SORA From Scratch: Diffusion Transformers for Video Generation Models](https://leetarxiv.substack.com/p/the-annotated-diffusion-transformer) - code first walkthrough of DiT, the architecture behind Sora
- [The Principles of Diffusion Models](https://arxiv.org/abs/2510.21890) - a full monograph tracing diffusion models from VAE/score/flow perspectives through flow map models, with a [companion site](https://the-principles-of-diffusion-models.github.io)
- [awesome-diffusion-models](https://github.com/hyungkwonko/awesome-diffusion-models) - curated papers and open source code if you want to go past the intros above

## Text-to-Image Personalization

A tight and unusually legible research thread from 2022 and 2023, all answering one question: how do you teach a pretrained text-to-image model a new subject without retraining it. It is worth reading as a group, because the field converged on encoders and low rank updates within about eighteen months, and the same answers turned up in LLM land shortly afterwards. See [Fine-Tuning and PEFT](../README.md#fine-tuning-and-peft) for the text side.

- [SDEdit: Guided Image Synthesis and Editing with Stochastic Differential Equations](https://arxiv.org/abs/2108.01073) - noise it partway, denoise it back. The simplest editing primitive and still in use
- [Key-Locked Rank One Editing for Text-to-Image Personalization](https://research.nvidia.com/labs/par/Perfusion/) - Perfusion, a 100KB personalization at rank one. The project page is better than the paper
- [HyperDreamBooth](https://hyperdreambooth.github.io/) - a hypernetwork that predicts the weight update instead of optimizing for it, so personalization drops from minutes to seconds
- [Domain-Agnostic Tuning-Encoder for Fast Personalization of Text-To-Image Models](https://arxiv.org/abs/2307.06925) - the encoder based approach generalized past the single-domain assumption
- [e4t-diffusion](https://github.com/mkshing/e4t-diffusion) - an implementation of the encoder based tuning work, for when the papers stop being enough

---

# The Recognition Thread

## Pre-Diffusion Classics

- [ImageNet Classification with Deep Convolutional Neural Networks](https://www.cs.toronto.edu/~kriz/imagenet_classification_with_deep_convolutional.pdf) - AlexNet, the 2012 paper that kicked off the deep learning era in computer vision, also on Ilya's reading list
- [Deep Residual Learning for Image Recognition](https://arxiv.org/abs/1512.03385) - ResNet, the skip connection paper, arguably still the most reused idea in all of deep learning
- [Faster R-CNN: Towards Real-Time Object Detection with Region Proposal Networks](https://arxiv.org/abs/1506.01497) - the object detection classic
- [An Image is Worth 16x16 Words: Transformers for Image Recognition at Scale](https://arxiv.org/abs/2010.11929) - ViT, transformers finally come for CV
- [Learning Transferable Visual Models From Natural Language Supervision](https://arxiv.org/abs/2103.00020) - CLIP, contrastive image/text pretraining
- [Sigmoid Loss for Language Image Pre-Training](https://arxiv.org/abs/2303.15343) - SigLIP, CLIP's successor, swaps the softmax contrastive loss for a sigmoid one

## Vision-Language Models (VLMs)

- [SigLIP 2: Multilingual Vision-Language Encoders with Improved Semantic Understanding, Localization, and Dense Features](https://arxiv.org/abs/2502.14786) - drop-in successor to SigLIP, adds captioning-based pretraining, self-distillation and masked prediction for stronger zero-shot and dense-prediction performance
- [Visual Instruction Tuning](https://arxiv.org/abs/2304.08485) - LLaVA, the original recipe for bolting a CLIP ViT onto an LLM via a small projector and instruction-tuning on GPT-4 generated multimodal data
- [PaliGemma 2: A Family of Versatile VLMs for Transfer](https://arxiv.org/abs/2412.03555) - pairs a SigLIP encoder with Gemma 2 across multiple sizes and resolutions, the same single-projection recipe as LLaVA but from Google
- [Gemma 3 Technical Report](https://arxiv.org/abs/2503.19786) - Google's first multimodal Gemma, adds a SigLIP-based vision tower with "pan and scan" cropping for high-res/non-square inputs
- [DeepSeek-VL2: Mixture-of-Experts Vision-Language Models for Advanced Multimodal Understanding](https://arxiv.org/abs/2412.10302) - dynamic tiling of high-res images/documents into a SigLIP-style tower feeding an MoE language model, deeper fusion than a single projection step
- [Qwen3-VL Technical Report](https://arxiv.org/abs/2511.21631) - multi-level vision features ("DeepStack") injected into several LLM layers instead of just the input, one of the current SOTA-ish open VLM families

## Video Understanding Models

- [Is Space-Time Attention All You Need for Video Understanding?](https://arxiv.org/abs/2102.05095) - TimeSformer, a convolution-free video classifier using divided space-time self-attention, an early "true 3D" video encoder
- [VideoMAE: Masked Autoencoders are Data-Efficient Learners for Self-Supervised Video Pre-Training](https://arxiv.org/abs/2203.12602) - adapts masked autoencoding to video with extreme tube masking, works well even on small datasets
- [InternVideo: General Video Foundation Models via Generative and Discriminative Learning](https://arxiv.org/abs/2212.03191) - combines masked video modeling with video-language contrastive learning; superseded by [InternVideo2](https://arxiv.org/abs/2403.15377)
