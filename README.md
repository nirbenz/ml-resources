# An Always*-Updating List of LLM/Language/Vision Resources

**when I feel like it*

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [Who Is This For?](#who-is-this-for)
- [Topics](#topics)
- [Technical and Science Stuff](#technical-and-science-stuff)
  - [Karpathy's "Building GPT From Scratch"](#karpathys-building-gpt-from-scratch)
  - [Understanding Transformers and Attention](#understanding-transformers-and-attention)
  - [NLP/LLM Academic Courses](#nlpllm-academic-courses)
  - [Training Large Models: War Stories](#training-large-models-war-stories)
  - [Curated Reading Lists](#curated-reading-lists)
- [Retrieval and RAG](#retrieval-and-rag)
  - [Memory (Not RAG)](#memory-not-rag)
- [Knowledge Graphs](#knowledge-graphs)
- [Agents](#agents)
- [Using LLMs](#using-llms)
  - [Prompt Engineering](#prompt-engineering)
  - [CoT](#cot)
  - [RL / Post-training in Practice](#rl--post-training-in-practice)
- [Reasoning](#reasoning)
  - [On AGI Timelines](#on-agi-timelines)
- [Computer Vision](#computer-vision)
  - [Diffusion Models](#diffusion-models)
  - [Pre-Diffusion Classics](#pre-diffusion-classics)
  - [Vision-Language Models (VLMs)](#vision-language-models-vlms)
  - [Video Understanding Models](#video-understanding-models)
- [MCP/Cursor](#mcpcursor)
  - [Claude Code](#claude-code)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Who Is This For?

The target audience is generally;
1. People who do Machine Learning in their current day to day, but are focused on topics which are *not* LLMs; Computer vision, data scientists, etc.
2. Engineers who are first walking into this world and want to mainly use LLMs as a tool (and hence are less concerned about how they work)

**Note** that I am intentionally *not* covering general ML and this isn't meant to be a crash course to using LLMs if you lack some necessary background.

## Topics

This is a shortlist of topics which I find important. I am not going to cover them all (or provide links) but they serve as a general purpose list of things I think *should be learned* in order to better use LLMs as tools.

When I come by a good resource for some of the topics here - I place it in this document.

The technical parts, specifically, can probably be skipped if you don't think you need to understand them.

1. The scientific/technical part.
   1. How language models work
   2. What are transformers? What is the attention mechanism? Why is it important?
   3. What makes a model "large"
   4. What are scaling laws?
   5. Why is training large models is so difficult/expensive?
   6. What is instruct tuning and Reinforcement Learning with Human Feedback (RLHF)?

2. Retrieval
   1. What is retrieval?
   2. RAG (Retrieval Augmented Generation)
   3. What are embeddings? What are *dense* embeddings? 
   4. What are classical embeddings and why are they still important (TF-IDF, BM25)?
   5. Reranking
   6. Approximate Nearest Neighbour, FAISS and vector databases

3. Knowledge Graphs
   1. What are knowledge graphs?
   2. When should I use a graphical data structure (conceptually)?
   3. How can I use LLMs to create large knowledge graphs?

4. Agentic Flows
   1. What are agents?

5. Using LLMs in Practice
   1. API models when how etc.
   2. When should I use self-hosted models and/or fine-tune?
   3. Common frameworks
   4. What constitutes "context"?
   5. How do I create better prompts?
   6. Chain of Thought

6. MCP/Cursor/Both
7. Reasoning
8. Computer Vision
   1. What are diffusion models and how do they work?
   2. What are Vision-Language Models (VLMs) and how do they extend to video?

---

## Technical and Science Stuff

### Karpathy's "Building GPT From Scratch"

If you are going to find the time for just one resource, this is by far the best and most
intuitive resources. As always with *Andrej Karpathy* - he is the master of explaining complex topics in Machine Learning related maths/engineering.

- [Karpathy's minimal GPT repo](https://github.com/karpathy/minGPT)
- [Let's build GPT: from scratch, in code, spelled out](https://www.youtube.com/watch?v=kCc8FmEb1nY)
- [Let's reproduce GPT-2 (124M)](https://www.youtube.com/watch?v=l8pRSuU81PU)

### Understanding Transformers and Attention

- [The Illustrated Transformer](https://jalammar.github.io/illustrated-transformer/) - the classic visual walkthrough, still the best starting point
- [The Illustrated GPT-2](https://jalammar.github.io/illustrated-gpt2/) - same treatment, applied to decoder-only models
- [The Annotated Transformer](https://nlp.seas.harvard.edu/annotated-transformer/)
- [Really deep dive into transformer inference arithmetic](https://kipp.ly/transformer-inference-arithmetic/#kv-cache)
- [Getting Meaning From Text: Self-Attention Step-by-Step](https://pub.towardsai.net/getting-meaning-from-text-self-attention-step-by-step-video-7d8f49694f89)
- [GPT in 60 Lines of NumPy](https://jaykmody.com/blog/gpt-from-scratch/)
- [Becoming the Unbeatable: How I Fine-Tuned GPT's KV Cache](https://dipkumar.dev/becoming-the-unbeatable/posts/gpt-kvcache/)
- [HG's Test Time Compute](https://huggingface.co/spaces/HuggingFaceH4/blogpost-scaling-test-time-compute)


### NLP/LLM Academic Courses
If you want to dedicate yourself to a full course in the field - here are some good options.
- [Stanford's current main NLP course](https://stanford-cs336.github.io/spring2025/)
- [Great list by Yoav Goldberg](https://gist.github.com/yoavg/95bbc5768cacd2bf07187779fada4867)

### Training Large Models: War Stories

- [OPT-175B Logbook](https://github.com/facebookresearch/metaseq/blob/main/projects/OPT/chronicles/OPT175B_Logbook.pdf) - Meta's day by day log of what it actually took to keep a 175B dense model training. The best antidote to anyone who thinks large scale training is easy

### Curated Reading Lists

Some of these are lists of lists - use them to go deeper than what's in this document.

- [a16z's AI Canon](https://a16z.com/ai-canon/) - a broad, tiered reading list from beginner explainers to deeply technical papers, covering LLMs, diffusion models and the AI market
- [Sebastian Raschka's "Understanding Large Language Models" reading list](https://sebastianraschka.com/blog/2023/llm-reading-list.html) - academic papers only, meant to be read chronologically
- Ilya Sutskever reportedly gave John Carmack this list of papers, saying "if you learn all of these, you'll know 90% of what matters today": [curated version with links to every paper](https://github.com/dzyim/ilya-sutskever-recommended-reading)

## Retrieval and RAG

- [Anthropic's blogpost on contextual retrieval](https://www.anthropic.com/news/contextual-retrieval) - this is an important resource!
- [Pinecone's comprehensive guide to vector indexes](https://www.pinecone.io/learn/series/faiss/vector-indexes/)
- [Pinecone on HNSW specifically](https://www.pinecone.io/learn/series/faiss/hnsw/)
- [Okapi BM25](https://en.wikipedia.org/wiki/Okapi_BM25)
- [Pinecone's take on rerankers](https://www.pinecone.io/learn/series/rag/rerankers/)

### Memory (Not RAG)

- [How does ChatGPT's memory actually work?](https://manthanguptaa.in/posts/chatgpt_memory/) - spoiler: no RAG involved

## Knowledge Graphs

- [awesome-knowledge-graph](https://github.com/totogo/awesome-knowledge-graph) - the canonical curated list: learning materials, databases, tools
- [Awesome-GraphRAG](https://github.com/DEEP-PolyU/Awesome-GraphRAG) - surveys, papers and open source projects specifically on graph based RAG, the most common answer to "why use a KG with an LLM"

## Agents

- [Anthropic's "Building Effective Agents"](https://www.anthropic.com/research/building-effective-agents) - the practical, opinionated take: start simple, only add agentic complexity when a workflow genuinely needs it
- [Lilian Weng's "LLM Powered Autonomous Agents"](https://lilianweng.github.io/posts/2023-06-23-agent/) - the theoretical framing: planning, memory and tool use as the three core components

## Using LLMs

### Prompt Engineering

- [DAIR.AI's Prompt Engineering Guide](https://www.promptingguide.ai/) - the most comprehensive one out there, also covers context engineering, RAG and agents

### CoT
- Original Paper: [Chain-of-Thought Prompting Elicits Reasoning in Large Language Models](https://arxiv.org/abs/2201.11903)
- [Google Research blog on chain of thought](https://research.google/blog/language-models-perform-reasoning-via-chain-of-thought/)
- [Anthropic's practical guide to chain of thought](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/chain-of-thought)
- [Anthropic on chain prompts](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/chain-prompts)

### RL / Post-training in Practice

- [Improving Cursor Tab with online RL](https://cursor.com/blog/tab-rl) - good case study showing plain policy gradient (not GRPO) is enough when you have a lot of on-policy data and solid infra

## Reasoning

- [Anthropic's Research on Reasoning Models](https://www.anthropic.com/research/tracing-thoughts-language-model)
- [Demystifying Reasoning Models](https://cameronrwolfe.substack.com/p/demystifying-reasoning-models)
- [Understanding the New Class of "Reasoning" LLMs](https://sebastianraschka.com/blog/2025/understanding-reasoning-llms.html)

### On AGI Timelines

- [Noam Brown on where AI researchers actually agree](https://x.com/polynoamial/status/1994439121243169176) - beyond the hype vs doom framing, most leading researchers agree the current paradigm is enough for massive impact, but a few more breakthroughs (continual learning, sample efficiency) are needed for AGI/ASI

## Computer Vision

### Diffusion Models

- [Lilian Weng's "What are Diffusion Models?"](https://lilianweng.github.io/posts/2021-07-11-diffusion-models/) - still the best first read on DDPMs, score based models and NCSN
- [The Annotated Diffusion Transformer](https://leetarxiv.substack.com/p/the-annotated-diffusion-transformer) - code first walkthrough of DiT, the architecture behind Sora
- [The Principles of Diffusion Models](https://arxiv.org/abs/2510.21890) - a full monograph tracing diffusion models from VAE/score/flow perspectives through flow map models, with a [companion site](https://the-principles-of-diffusion-models.github.io)
- [awesome-diffusion-models](https://github.com/hyungkwonko/awesome-diffusion-models) - curated papers and open source code if you want to go past the intros above

### Pre-Diffusion Classics

- [ImageNet Classification with Deep Convolutional Neural Networks](https://www.cs.toronto.edu/~kriz/imagenet_classification_with_deep_convolutional.pdf) - AlexNet, the 2012 paper that kicked off the deep learning era in computer vision, also on Ilya's reading list above
- [Deep Residual Learning for Image Recognition](https://arxiv.org/abs/1512.03385) - ResNet, the skip connection paper, arguably still the most reused idea in all of deep learning
- [Faster R-CNN: Towards Real-Time Object Detection with Region Proposal Networks](https://arxiv.org/abs/1506.01497) - the object detection classic
- [An Image is Worth 16x16 Words: Transformers for Image Recognition at Scale](https://arxiv.org/abs/2010.11929) - ViT, transformers finally come for CV
- [Learning Transferable Visual Models From Natural Language Supervision](https://arxiv.org/abs/2103.00020) - CLIP, contrastive image/text pretraining
- [Sigmoid Loss for Language Image Pre-Training](https://arxiv.org/abs/2303.15343) - SigLIP, CLIP's successor, swaps the softmax contrastive loss for a sigmoid one

### Vision-Language Models (VLMs)

- [SigLIP 2: Multilingual Vision-Language Encoders with Improved Semantic Understanding, Localization, and Dense Features](https://arxiv.org/abs/2502.14786) - drop-in successor to SigLIP, adds captioning-based pretraining, self-distillation and masked prediction for stronger zero-shot and dense-prediction performance
- [Visual Instruction Tuning](https://arxiv.org/abs/2304.08485) - LLaVA, the original recipe for bolting a CLIP ViT onto an LLM via a small projector and instruction-tuning on GPT-4 generated multimodal data
- [PaliGemma 2: A Family of Versatile VLMs for Transfer](https://arxiv.org/abs/2412.03555) - pairs a SigLIP encoder with Gemma 2 across multiple sizes and resolutions, the same single-projection recipe as LLaVA but from Google
- [Gemma 3 Technical Report](https://arxiv.org/abs/2503.19786) - Google's first multimodal Gemma, adds a SigLIP-based vision tower with "pan and scan" cropping for high-res/non-square inputs
- [DeepSeek-VL2: Mixture-of-Experts Vision-Language Models for Advanced Multimodal Understanding](https://arxiv.org/abs/2412.10302) - dynamic tiling of high-res images/documents into a SigLIP-style tower feeding an MoE language model, deeper fusion than a single projection step
- [Qwen3-VL Technical Report](https://arxiv.org/abs/2511.21631) - multi-level vision features ("DeepStack") injected into several LLM layers instead of just the input, one of the current SOTA-ish open VLM families

### Video Understanding Models

- [Is Space-Time Attention All You Need for Video Understanding?](https://arxiv.org/abs/2102.05095) - TimeSformer, a convolution-free video classifier using divided space-time self-attention, an early "true 3D" video encoder
- [VideoMAE: Masked Autoencoders are Data-Efficient Learners for Self-Supervised Video Pre-Training](https://arxiv.org/abs/2203.12602) - adapts masked autoencoding to video with extreme tube masking, works well even on small datasets
- [InternVideo: General Video Foundation Models via Generative and Discriminative Learning](https://arxiv.org/abs/2212.03191) - combines masked video modeling with video-language contrastive learning; superseded by [InternVideo2](https://arxiv.org/abs/2403.15377)

## MCP/Cursor

- [cursor-mcp-examples](https://github.com/nirbenz/cursor-mcp-examples) (this was written by me)
- [Cursor's docs on tools](https://docs.cursor.com/tools)
- [Cursor's docs on rules](https://docs.cursor.com/context/rules)
- [Cursor Custom Agents Rules Generator](https://github.com/bmadcode/cursor-custom-agents-rules-generator)
- [Big collection of cursor rules](https://github.com/PatrickJS/awesome-cursorrules)
- [awesome-mcp-servers](https://github.com/wong2/awesome-mcp-servers) - curated list of MCP servers, the equivalent list for the MCP side
- [GitHub's MCP server](https://github.com/github/github-mcp-server)
- [Model Context Protocol Python SDK](https://github.com/modelcontextprotocol/python-sdk)
- [Linear's MCP Integration Announcement](https://linear.app/changelog/2025-05-01-mcp)

### Claude Code

- [Boris Cherny's Claude Code tips thread](https://x.com/bcherny/status/2017742741636321619) - from the creator of Claude Code: run 3-5 git worktrees in parallel, invest heavily in CLAUDE.md, write custom skills, use plan mode for complex tasks, use subagents to keep main context clean