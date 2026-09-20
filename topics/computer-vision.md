# Computer Vision

Part of [An Always*-Updating List of LLM/Language/Vision Resources](../README.md).

Three threads in here, mostly independent, plus a history section at the end.

The **generative** one is what people usually want; VAEs, GANs, diffusion, rectified flow, then the 2023 rush to personalize text-to-image models cheaply. Roughly in the order the field figured things out, because diffusion doesn't really make sense until you've seen a VAE, the VQ part of modern image tokenizers comes straight out of the GAN era, and flow matching is much easier to get once you already understand diffusion.

The **recognition** one is about encoders and what you do with them; picking a visual backbone, then VLMs, then video.

The **3D** one is small - novel view synthesis, which is its own world and barely touches the other two.

Everything historical sits in [History, For the Curious](#history-for-the-curious) at the bottom. Read it if you want to know how the field got here, skip it if you just want what works now.

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [The Generative Thread](#the-generative-thread)
  - [VAEs and Variational Inference](#vaes-and-variational-inference)
  - [GANs](#gans)
  - [From VAEs to Diffusion](#from-vaes-to-diffusion)
  - [Diffusion Models](#diffusion-models)
  - [Rectified Flow and Flow Matching](#rectified-flow-and-flow-matching)
  - [Text-to-Image Personalization](#text-to-image-personalization)
- [The Recognition Thread](#the-recognition-thread)
  - [Choosing a Visual Encoder](#choosing-a-visual-encoder)
  - [Vision-Language Models (VLMs)](#vision-language-models-vlms)
  - [Video Understanding Models](#video-understanding-models)
- [3D and Novel View Synthesis](#3d-and-novel-view-synthesis)
- [History, For the Curious](#history-for-the-curious)
  - [Backbones](#backbones)
  - [Detection and Segmentation](#detection-and-segmentation)
  - [Representation Learning](#representation-learning)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

---

# The Generative Thread

If you'd rather read one thing that covers the whole arc before starting on any of it, [Diffusion Models - bit by bit](https://www.himanshustwts.com/posts/diffusion) goes generative modelling - GANs - VAEs as setup for diffusion, in one narrative. Conceptual and mathematical, no code.

## VAEs and Variational Inference

The autoencoder part is obvious. The *variational* part is where people lose it - and it's worth not losing, because the ELBO shows up again in diffusion, and the encoder/decoder pair shows up again as the thing Stable Diffusion actually runs inside.

- [From Autoencoder to Beta-VAE](https://lilianweng.github.io/posts/2018-08-12-vae/) - start here. Goes autoencoder - denoising - sparse - VAE - beta-VAE - VQ-VAE, and that last step leads straight into VQGAN below
- [Auto-Encoding Variational Bayes](https://arxiv.org/abs/1312.6114) - Kingma and Welling, the original
- [An Introduction to Variational Autoencoders](https://arxiv.org/abs/1906.02691) - the same authors explaining their own work at monograph length six years later. A much gentler step than the paper
- [Variational Auto-Encoders and the Expectation-Maximization Algorithm](https://maurocamaraescudero.netlify.app/post/variational-auto-encoders-and-the-expectation-maximization-algorithm/) - the connection to EM, which most tutorials skip entirely

Two questions everyone hits partway through the derivation:

- [Why do we start from KL(q(z)||p(z|x)) in the ELBO derivation?](https://stats.stackexchange.com/questions/531503/why-do-we-start-from-kldqz-pzx-in-elbo-derivation)
- [Why does maximizing the lower bound maximize the probability?](https://stats.stackexchange.com/questions/315841/why-maximizing-the-lower-bound-of-variational-evidence-maximizes-the-probability)

And if the KL term itself is the part that isn't landing, [Understanding KL Divergence in Diffusion Generative Models and Beyond](https://www.himanshustwts.com/posts/dgm-kl-divergence) builds it up properly rather than assuming it.

## GANs

Nobody trains GANs anymore. Read this anyway - adversarial training is where the field learned what genuinely unstable optimization feels like, mode collapse is still the canonical failure mode for any generative objective, and VQGAN is the direct ancestor of basically every image tokenizer in use today.

- [How to Train a GAN (ganhacks)](https://github.com/soumith/ganhacks) - a list of superstitions from NIPS 2016. The best surviving artifact of what training these things was actually like
- [Image-to-Image Translation with Conditional Adversarial Networks](https://arxiv.org/abs/1611.07004) - pix2pix. Conditional generation is the idea that survived more or less intact into ControlNet
- [Taming Transformers for High-Resolution Image Synthesis](https://arxiv.org/abs/2012.09841) - VQGAN. Discrete latents plus a transformer prior, which is still the recipe behind current image and video tokenizers
- [The Illustrated VQGAN](https://ljvmiranda921.github.io/notebook/2021/08/08/clip-vqgan/) - the readable version of the above, plus the CLIP-guided variant that briefly ate the internet in 2021
- [Limitations of Encoder-Decoder GAN architectures](http://www.offconvex.org/2018/03/12/bigan/) - Arora on why BiGAN can't learn the representations it was claimed to. It's theory, so it hasn't aged

## From VAEs to Diffusion

- [Diffusion Models as a kind of VAE](https://angusturner.github.io/generative_models/2021/06/29/diffusion-probabilistic-models-I.html) - the bridge. If the previous section landed, this reframes DDPM as a hierarchical VAE with a fixed encoder and the whole thing clicks
- [Diffusion models are autoencoders](https://sander.ai/2022/01/31/diffusion.html) - Dieleman making the same connection from the other side, and much shorter
- [How AI Image Generators Work (Computerphile)](https://www.youtube.com/watch?v=1CIpzeNxIhU) - fifteen minutes, no maths, and correct. Good for people who don't want any of the above

## Diffusion Models

- [Lilian Weng's "What are Diffusion Models?"](https://lilianweng.github.io/posts/2021-07-11-diffusion-models/) - still the best first read on DDPMs, score based models and NCSN
- [Understanding Diffusion Models: A Unified Perspective](https://calvinyluo.com/2022/08/26/diffusion-tutorial.html) - Calvin Luo deriving all of it from the ELBO; hierarchical VAEs, the three equivalent interpretations of what the network is predicting, score matching, then classifier and classifier-free guidance. Every step is actually written out, so if the math in the papers loses you this is the one that doesn't. PDF version on the same page
- [Diffusion Models From Scratch](https://www.tonyduan.com/diffusion/index.html) - Tony Duan, roughly a lecture per page, with a 500 line MNIST codebase to match. Goes past where most intros stop; DDPM vs DDIM, noise schedules, the Karras parameterization and the advanced solvers
- [High-Resolution Image Synthesis with Latent Diffusion Models](https://arxiv.org/abs/2112.10752) - LDM, the Stable Diffusion paper. Run diffusion in a VAE's latent space instead of pixel space and the compute drops by orders of magnitude. This is the single architectural decision that put image generation on consumer GPUs
- [SORA From Scratch: Diffusion Transformers for Video Generation Models](https://leetarxiv.substack.com/p/the-annotated-diffusion-transformer) - code first walkthrough of DiT, the architecture behind Sora
- [Perspectives on diffusion](https://sander.ai/2023/07/20/perspectives.html) - Dieleman showing diffusion models are autoencoders, latent variable models, score predictors, reverse SDE solvers, flow models, RNNs and autoregressive models, all at once. Very good for making separate papers stop looking like separate fields
- [The Principles of Diffusion Models](https://arxiv.org/abs/2510.21890) - a full monograph tracing diffusion models from VAE/score/flow perspectives through flow map models, with a [companion site](https://the-principles-of-diffusion-models.github.io). Now at v3, which adds a discrete diffusion chapter and per-chapter reader guides ahead of MIT Press publication
- [ConceptAttention: Diffusion Transformers Learn Highly Interpretable Features](https://arxiv.org/abs/2502.04320) - DiTs align text and image representations as a byproduct of conditional denoising, so a dot product between the two gives you sharp saliency maps for free. Beats CLIP at segmentation, with no training at all ([project page](https://alechelbling.com/ConceptAttention/))
- [awesome-diffusion-models](https://github.com/hyungkwonko/awesome-diffusion-models) - curated papers and open source code if you want to go past the intros above

## Rectified Flow and Flow Matching

Diffusion isn't how the strongest image models get trained anymore. Flow matching reframes generation as learning a velocity field that moves noise to data, and rectified flow is the variant that straightens those paths out so you can sample in way fewer steps. SD3 and FLUX are both built on it.

The important thing to get early; this is a change of coordinates, not a rival framework. Read the first two and you stop reading the diffusion and flow literature as if they were two separate fields.

- [Diffusion Meets Flow Matching: Two Sides of the Same Coin](https://diffusionflow.github.io/) - start here. Walks through the equivalence explicitly, which saves a lot of confusion later
- [Visualizing Rectified Flows](https://alechelbling.com/blog/rectified-flow/) - interactive, and it runs a real flow model in your browser. Why flow models learn curved trajectories, why that costs you sampling steps, and what reflow does about it. Much easier to get the geometric intuition here than from the papers. Code in [Diffusion-Explorer](https://github.com/helblazer811/Diffusion-Explorer)
- [Flow Straight and Fast: Learning to Generate and Transfer Data with Rectified Flow](https://arxiv.org/abs/2209.03003) - rectified flow itself, plus the reflow procedure
- [Flow Matching for Generative Modeling](https://arxiv.org/abs/2210.02747) - Lipman et al.'s parallel formulation, arrived at independently. This is the more common vocabulary now
- [Scaling Rectified Flow Transformers for High-Resolution Image Synthesis](https://arxiv.org/abs/2403.03206) - SD3. The paper that took this mainstream for text-to-image, and the best account of what actually matters at scale
- [FLUX.1](https://github.com/black-forest-labs/flux) - Black Forest Labs' inference repo, and the strongest open weights model in this lineage. The [launch post](https://bfl.ai/announcements/24-08-01-bfl) stands in for a paper on the original release
- [FLUX.1 Kontext: Flow Matching for In-Context Image Generation and Editing in Latent Space](https://arxiv.org/abs/2506.15742) - the FLUX work that does have a paper, and the in-context editing story
- [Flow Matching Guide and Code](https://arxiv.org/abs/2412.06264) - Meta's monograph, with implementations. For when you want the full treatment

## Text-to-Image Personalization

A tight, unusually readable research thread from 2022-2023, all answering one question; how do you teach a pretrained text-to-image model a new subject without retraining it. Worth reading as a group - the field converged on encoders and low rank updates in about eighteen months, and the same answers showed up in LLM land shortly after. See [Fine-Tuning and PEFT](../README.md#fine-tuning-and-peft) for the text side.

- [SDEdit: Guided Image Synthesis and Editing with Stochastic Differential Equations](https://arxiv.org/abs/2108.01073) - noise it partway, denoise it back. Simplest editing primitive there is, and still in use
- [Key-Locked Rank One Editing for Text-to-Image Personalization](https://research.nvidia.com/labs/par/Perfusion/) - Perfusion. 100KB personalization at rank one, and the project page is frankly better than the paper
- [HyperDreamBooth](https://hyperdreambooth.github.io/) - a hypernetwork that predicts the weight update instead of optimizing for it. Personalization drops from minutes to seconds
- [Domain-Agnostic Tuning-Encoder for Fast Personalization of Text-To-Image Models](https://arxiv.org/abs/2307.06925) - the encoder based approach, generalized past the single-domain assumption

---

# The Recognition Thread

For a single talk covering where this whole thread ended up, [Vision in the Age of LLMs](https://www.youtube.com/watch?v=0XB7fNS_ONg) is Lucas Beyer at ETH Zurich in 2026. He co-authored ViT, SigLIP and PaliGemma, so most of the encoders below are his.

## Choosing a Visual Encoder

Not every vision backbone is doing the same job, and picking the wrong one is a very common quiet mistake. Roughly;

- CLIP/SigLIP are trained over image+text (alt-text) pairs, so their embeddings are much more "semantic sensitive" than "geometric sensitive"
- DINOv2/3 is a general purpose feature extractor, with no language supervision at all
- Copy detection models like SSCD are trained for geometric transformations

"Is this the same scene" and "is this the same shot, re-encoded" are different questions, and they want different encoders.

- [Learning Transferable Visual Models From Natural Language Supervision](https://arxiv.org/abs/2103.00020) - CLIP, contrastive image/text pretraining
- [Sigmoid Loss for Language Image Pre-Training](https://arxiv.org/abs/2303.15343) - SigLIP, CLIP's successor, swaps the softmax contrastive loss for a sigmoid one
- [DINOv2: Learning Robust Visual Features without Supervision](https://arxiv.org/abs/2304.07193) - self-supervised features that transfer without fine-tuning. The default when you want a general purpose extractor rather than a semantic one
- [DINOv3](https://arxiv.org/abs/2508.10104) - the current generation, scaled up
- [A Self-Supervised Descriptor for Image Copy Detection](https://arxiv.org/abs/2202.10261) - SSCD, the geometric end of the spectrum. Worth knowing it exists so you stop reaching for a semantic encoder when what you actually wanted was a fingerprint

## Vision-Language Models (VLMs)

VLMs operate on images and text at the same time. Pretty loose term, yes. Three generations of connector design, worth reading in order because each one is a reaction to the previous:

1. **Cross-attention into a frozen LLM.** Flamingo interleaves gated cross-attention layers into a frozen language model.
2. **Project into the token stream.** Either through a learned bottleneck (BLIP-2's Q-Former) or just a linear projection (LLaVA). Visual tokens go in once, at the input.
3. **Deep fusion.** Patch tokens from multiple encoder depths, injected at multiple LLM layers, plus tiling or cropping so resolution survives. Qwen3-VL, DeepSeek-VL2 and Gemma 3 all do versions of this.

I like the third generation most, for two reasons; the model sees multiple views of a scene instead of one squashed 224x224, and the LLM gets visual info at multiple depths so it can keep going back to the evidence, instead of working off a single pooled embedding.


- [Flamingo: a Visual Language Model for Few-Shot Learning](https://arxiv.org/abs/2204.14198) - generation one, and where interleaved image-text prompting comes from. Most of what followed is arguably a simplification of it
- [BLIP-2: Bootstrapping Language-Image Pre-training with Frozen Image Encoders and Large Language Models](https://arxiv.org/abs/2301.12597) - the Q-Former. A learned bottleneck that squeezes patch tokens down to a small fixed set before the LLM sees them, and the main alternative to LLaVA's linear projection
- [Qwen2-VL: Enhancing Vision-Language Model's Perception of the World at Any Resolution](https://arxiv.org/abs/2409.12191) - naive dynamic resolution and M-RoPE, which is where the "any-res" handling in the current generation comes from. Read it before the Qwen3-VL report
- [SigLIP Paper - hola sigmoid!](https://www.himanshustwts.com/posts/siglip) - walks contrastive pre-training, why the sigmoid loss matters and what the architecture actually does. Easier entry than the paper if SigLIP is the bit you care about
- [SigLIP 2: Multilingual Vision-Language Encoders with Improved Semantic Understanding, Localization, and Dense Features](https://arxiv.org/abs/2502.14786) - drop-in successor to SigLIP, adds captioning-based pretraining, self-distillation and masked prediction for stronger zero-shot and dense-prediction performance
- [Visual Instruction Tuning](https://arxiv.org/abs/2304.08485) - LLaVA, the original recipe for bolting a CLIP ViT onto an LLM via a small projector and instruction-tuning on GPT-4 generated multimodal data
- [PaliGemma 2: A Family of Versatile VLMs for Transfer](https://arxiv.org/abs/2412.03555) - pairs a SigLIP encoder with Gemma 2 across multiple sizes and resolutions, the same single-projection recipe as LLaVA but from Google
- [Gemma 3 Technical Report](https://arxiv.org/abs/2503.19786) - Google's first multimodal Gemma, adds a SigLIP-based vision tower with "pan and scan" cropping for high-res/non-square inputs
- [DeepSeek-VL2: Mixture-of-Experts Vision-Language Models for Advanced Multimodal Understanding](https://arxiv.org/abs/2412.10302) - dynamic tiling of high-res images/documents into a SigLIP-style tower feeding an MoE language model, deeper fusion than a single projection step
- [Qwen3-VL Technical Report](https://arxiv.org/abs/2511.21631) - multi-level vision features ("DeepStack") injected into several LLM layers instead of just the input, one of the current SOTA-ish open VLM families

## Video Understanding Models

How image encoders become video encoders, in practice. Four families, in increasing order of cost and temporal fidelity:

1. **Sample and pool.** Sample N frames (say 0.5fps), run each through a 2D ViT, pool across time. Cheap, off the shelf backbone, no temporal structure at all. Still very common.
2. **Sample and concatenate.** Keep every frame's patch tokens, concatenate them with frame separators and temporal position encodings. Temporal reasoning gets delegated to the language model, which at least now has explicit temporal structure in its input.
3. **Temporal connector.** A learned module pools across time between the vision encoder and the LLM, so tokens are already motion-aware by the time the LLM sees them. This is where most things are.
4. **True space-time encoders.** Treat video as a 3D tensor from the start, attention factorized into spatial and temporal. Best and most direct approach.

Level 4 is also the least used. Compute is way higher, and pretraining at CLIP/SigLIP scale needs paired (video, text) data with timing, not just (image, caption) - so reusing existing ViTs isn't really an option. Because of that, most current open VLMs are levels 1-3, and they get temporal reasoning by cheating; sample frames, mark them with timestamps, let the LLM work out the sequence logic.

Below is the level 4 lineage, plus the transfer recipe most level 2 systems actually use.

- [LLaVA-OneVision: Easy Visual Task Transfer](https://arxiv.org/abs/2408.03326) - the clearest account of moving an image-trained VLM to video by just treating frames as more tokens. Level 2, done properly
- [Is Space-Time Attention All You Need for Video Understanding?](https://arxiv.org/abs/2102.05095) - TimeSformer, a convolution-free video classifier using divided space-time self-attention, an early "true 3D" video encoder
- [VideoMAE: Masked Autoencoders are Data-Efficient Learners for Self-Supervised Video Pre-Training](https://arxiv.org/abs/2203.12602) - adapts masked autoencoding to video with extreme tube masking, works well even on small datasets
- [InternVideo: General Video Foundation Models via Generative and Discriminative Learning](https://arxiv.org/abs/2212.03191) - combines masked video modeling with video-language contrastive learning; superseded by [InternVideo2](https://arxiv.org/abs/2403.15377)

---

# 3D and Novel View Synthesis

Small thread, and mostly disconnected from the other two; the goal is reconstructing and rendering a scene rather than recognizing or generating images. Included because it is a large part of modern computer vision that nothing else in this file touches.

- [NeRF: Representing Scenes as Neural Radiance Fields for View Synthesis](https://arxiv.org/abs/2003.08934) - encode a whole scene in the weights of a small MLP and render it by marching rays through that field. Beautiful, and painfully slow
- [3D Gaussian Splatting for Real-Time Radiance Field Rendering](https://arxiv.org/abs/2308.04079) - the same problem solved with explicit primitives and a rasterizer instead of an implicit field. Real-time rendering, much faster training, and it largely displaced NeRF in practice

---

# History, For the Curious

How the field got here. None of this is required to use anything above, but the lineage explains a lot of the design decisions that otherwise look arbitrary.

Grouped by what each line of work was actually trying to do, rather than strictly by date. Chronological within each group.

## Backbones

- [ImageNet Classification with Deep Convolutional Neural Networks](https://www.cs.toronto.edu/~kriz/imagenet_classification_with_deep_convolutional.pdf) - AlexNet, the 2012 paper that kicked off the deep learning era in computer vision, also on Ilya's reading list
- [Very Deep Convolutional Networks for Large-Scale Image Recognition](https://arxiv.org/abs/1409.1556) - VGG. Mostly remembered for showing depth with tiny 3x3 filters was the whole trick, and then for being the feature extractor everyone used for years afterwards - perceptual loss, style transfer, all of it
- [Going Deeper with Convolutions](https://arxiv.org/abs/1409.4842) - GoogLeNet/Inception. Parallel filter sizes in one block and aggressive 1x1 bottlenecks, which is where "just make it wider, not only deeper" starts
- [Deep Residual Learning for Image Recognition](https://arxiv.org/abs/1512.03385) - ResNet, the skip connection paper, arguably still the most reused idea in all of deep learning
- [An Image is Worth 16x16 Words: Transformers for Image Recognition at Scale](https://arxiv.org/abs/2010.11929) - ViT, transformers finally come for CV

## Detection and Segmentation

- [Faster R-CNN: Towards Real-Time Object Detection with Region Proposal Networks](https://arxiv.org/abs/1506.01497) - the object detection classic
- [You Only Look Once: Unified, Real-Time Object Detection](https://arxiv.org/abs/1506.02640) - YOLO. Detection as one regression pass instead of region proposals; the other branch from Faster R-CNN, and the one that won on speed
- [Focal Loss for Dense Object Detection](https://arxiv.org/abs/1708.02002) - RetinaNet. The insight is the loss, not the architecture; down-weight the easy background boxes and one-stage detection catches up with two-stage
- [U-Net: Convolutional Networks for Biomedical Image Segmentation](https://arxiv.org/abs/1505.04597) - written for biomedical segmentation, then spent years as the backbone of every diffusion model. Skip connections again
- [Mask R-CNN](https://arxiv.org/abs/1703.06870) - Faster R-CNN plus a mask head. The paper that made instance segmentation routine
- [Segment Anything](https://arxiv.org/abs/2304.02643) - SAM. Promptable segmentation trained on a billion masks, and segmentation's foundation model moment

## Representation Learning

Learning an embedding space where distance means something, rather than learning a classifier.

- [A Simple Framework for Contrastive Learning of Visual Representations](https://arxiv.org/abs/2002.05709) - SimCLR. Augment an image two ways, pull the pair together, push everything else apart. The augmentations turned out to matter more than the architecture did
- [Emerging Properties in Self-Supervised Vision Transformers](https://arxiv.org/abs/2104.14294) - the original DINO. Self-distillation with no labels, and the result nobody was expecting; the attention maps segment objects on their own. See [Choosing a Visual Encoder](#choosing-a-visual-encoder) for where this ended up
- [ArcFace: Additive Angular Margin Loss for Deep Face Recognition](https://arxiv.org/abs/1801.07698) - supervised, but the point is the geometry of the embedding rather than the classification. Still the default starting point for a lot of retrieval work, not only faces
