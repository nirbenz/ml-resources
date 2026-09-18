# An Always*-Updating List of LLM/Language/Vision Resources

**when I feel like it*

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

  - [Who Is This For?](#who-is-this-for)
  - [Topics](#topics)
- [Applied LLM Engineering](#applied-llm-engineering)
  - [Prompt Engineering](#prompt-engineering)
  - [Chain of Thought](#chain-of-thought)
  - [Context](#context)
  - [Retrieval and RAG](#retrieval-and-rag)
    - [Memory (Not RAG)](#memory-not-rag)
  - [Knowledge Graphs](#knowledge-graphs)
  - [Agents](#agents)
  - [Fine-Tuning and PEFT](#fine-tuning-and-peft)
  - [RL / Post-training in Practice](#rl--post-training-in-practice)
  - [Tooling](#tooling)
  - [MCP/Cursor](#mcpcursor)
    - [Claude Code](#claude-code)
- [LLM Science](#llm-science)
  - [Karpathy's "Building GPT From Scratch"](#karpathys-building-gpt-from-scratch)
  - [Understanding Transformers and Attention](#understanding-transformers-and-attention)
  - [Normalization](#normalization)
  - [Before Decoders: The Encoder Era](#before-decoders-the-encoder-era)
  - [Reasoning](#reasoning)
    - [On AGI Timelines](#on-agi-timelines)
  - [NLP/LLM Academic Courses](#nlpllm-academic-courses)
  - [Training Large Models: War Stories](#training-large-models-war-stories)
  - [Curated Reading Lists](#curated-reading-lists)
- [Computer Vision](#computer-vision)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Who Is This For?

The target audience is generally;
1. People who do Machine Learning in their current day to day, but are focused on topics which are *not* LLMs; Computer vision, data scientists, etc.
2. Engineers who are first walking into this world and want to mainly use LLMs as a tool (and hence are less concerned about how they work)

**Note** that I am intentionally *not* covering general ML and this isn't meant to be a crash course to using LLMs if you lack some necessary background.

## Topics

This is a shortlist of topics which I find important. I am not going to cover them all (or provide links) but they serve as a general purpose list of things I think *should be learned* in order to better use LLMs as tools.

When I come by a good resource for some of the topics here - I place it in this document.

The document is split three ways; [Applied LLM Engineering](#applied-llm-engineering) is about *using* models, [LLM Science](#llm-science) is about how they actually work, and [Computer Vision](#computer-vision) is its own thing - you either care about it or you don't. The science parts, specifically, can probably be skipped if you don't think you need to understand them.

1. Applied LLM Engineering
   1. How do I create better prompts?
   2. Chain of Thought
   3. What constitutes "context"? Why can't I just ask for more of it?
   4. What is retrieval? What is RAG (Retrieval Augmented Generation)?
   5. What are embeddings? What are *dense* embeddings?
   6. What are classical embeddings and why are they still important (TF-IDF, BM25)?
   7. Reranking
   8. Approximate Nearest Neighbour, FAISS and vector databases
   9. What are knowledge graphs? When should I use a graphical data structure (conceptually)?
   10. How can I use LLMs to create large knowledge graphs?
   11. What are agents?
   12. API models when how etc. Common frameworks
   13. When should I use self-hosted models and/or fine-tune?
   14. MCP/Cursor/Both

2. LLM Science
   1. How language models work
   2. What are transformers? What is the attention mechanism? Why is it important?
   3. What makes a model "large"
   4. What are scaling laws?
   5. Why is training large models is so difficult/expensive?
   6. What is instruct tuning and Reinforcement Learning with Human Feedback (RLHF)?
   7. What are reasoning models actually doing? What is test-time compute?

3. Computer Vision
   1. What are diffusion models and how do they work? What replaced them?
   2. What are Vision-Language Models (VLMs) and how do they extend to video?
   3. Where did all of this come from (VAEs, GANs)?

---

# Applied LLM Engineering

The practical part - using models, not understanding them. If you only read one section, read this one.

## Prompt Engineering

- [DAIR.AI's Prompt Engineering Guide](https://www.promptingguide.ai/) - the most comprehensive one out there, also covers context engineering, RAG and agents

## Chain of Thought

- Original Paper: [Chain-of-Thought Prompting Elicits Reasoning in Large Language Models](https://arxiv.org/abs/2201.11903)
- [Google Research blog on chain of thought](https://research.google/blog/language-models-perform-reasoning-via-chain-of-thought/)
- [Anthropic's prompting best practices](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices) - the separate chain-of-thought and chain-prompts pages both live here now, under "leverage thinking" and "chain complex prompts"

## Context

- [Extending Context is Hard](https://kaiokendev.github.io/context) - written back in the SuperHOT days, before position interpolation was even a paper. Still the best explanation of why you can't just raise the context number and expect things to work

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

## Fine-Tuning and PEFT

- [Parameter-Efficient Fine-Tuning (PEFT) for LLMs: A Comprehensive Introduction](https://towardsdatascience.com/parameter-efficient-fine-tuning-peft-for-llms-a-comprehensive-introduction-e52d03117f95) - good survey of the space; adapters, prefix tuning, LoRA
- [minLoRA](https://github.com/changjonathanc/minLoRA) - minimal PyTorch implementation, applies LoRA to any model. Read it once and LoRA stops being magic

**Note** that most of the early interesting work here actually happened in text-to-image, not text - see [Text-to-Image Personalization](topics/computer-vision.md#text-to-image-personalization).

## RL / Post-training in Practice

- [Improving Cursor Tab with online RL](https://cursor.com/blog/tab-rl) - good case study showing plain policy gradient (not GRPO) is enough when you have a lot of on-policy data and solid infra

## Tooling

- [Hugging Face pipelines](https://huggingface.co/docs/transformers/main_classes/pipelines) - still the fastest way to get from nothing to a running model. Start here before reaching for anything heavier

## MCP/Cursor

- [cursor-mcp-examples](https://github.com/nirbenz/cursor-mcp-examples) (this was written by me)
- [Cursor's docs](https://cursor.com/docs) - agents, rules, MCP, CLI. The old deep links to specific pages don't resolve anymore
- [BMAD-METHOD](https://github.com/bmad-code-org/BMAD-METHOD) - started life as a Cursor rules generator and grew into a full agentic dev framework. Very opinionated about how to structure agent work
- [Big collection of cursor rules](https://github.com/PatrickJS/awesome-cursorrules)
- [awesome-mcp-servers](https://github.com/wong2/awesome-mcp-servers) - curated list of MCP servers, the equivalent list for the MCP side
- [GitHub's MCP server](https://github.com/github/github-mcp-server)
- [Model Context Protocol Python SDK](https://github.com/modelcontextprotocol/python-sdk)
- [Linear's MCP Integration Announcement](https://linear.app/changelog/2025-05-01-mcp)

### Claude Code

- [Boris Cherny's Claude Code tips thread](https://x.com/bcherny/status/2017742741636321619) - from the creator of Claude Code: run 3-5 git worktrees in parallel, invest heavily in CLAUDE.md, write custom skills, use plan mode for complex tasks, use subagents to keep main context clean

---

# LLM Science

## Karpathy's "Building GPT From Scratch"

If you are going to find the time for just one resource, this is by far the best and most
intuitive resources. As always with *Andrej Karpathy* - he is the master of explaining complex topics in Machine Learning related maths/engineering.

- [Karpathy's minimal GPT repo](https://github.com/karpathy/minGPT)
- [Let's build GPT: from scratch, in code, spelled out](https://www.youtube.com/watch?v=kCc8FmEb1nY)
- [Let's reproduce GPT-2 (124M)](https://www.youtube.com/watch?v=l8pRSuU81PU)

## Understanding Transformers and Attention

- [The Illustrated Transformer](https://jalammar.github.io/illustrated-transformer/) - the classic visual walkthrough, still the best starting point
- [The Illustrated GPT-2](https://jalammar.github.io/illustrated-gpt2/) - same treatment, applied to decoder-only models
- [The Annotated Transformer](https://nlp.seas.harvard.edu/annotated-transformer/)
- [Really deep dive into transformer inference arithmetic](https://kipp.ly/transformer-inference-arithmetic/#kv-cache)
- [GPT in 60 Lines of NumPy](https://jaykmody.com/blog/gpt-from-scratch/)
- [Becoming the Unbeatable: How I Fine-Tuned GPT's KV Cache](https://dipkumar.dev/becoming-the-unbeatable/posts/gpt-kvcache/)

## Normalization

Small topic, but it's the first thing that looks arbitrary when you read a transformer implementation - and the answer is actually interesting.

- [Why do transformers use layer norm instead of batch norm?](https://stats.stackexchange.com/questions/474440/why-do-transformers-use-layer-norm-instead-of-batch-norm) - the question everyone hits, answered properly
- [Deep Learning normalization methods](https://tungmphung.com/deep-learning-normalization-methods/) - batch, layer, instance and group norm side by side, with the maths

## Before Decoders: The Encoder Era

BERT and friends aren't what anyone means by "LLM" today, but a lot of practical text-to-vector work still lives here. The architecture arguments are also much easier to follow at this scale.

- [How to get meaning from text with language model BERT](https://www.youtube.com/watch?v=-9vVhYEXeyQ) - solid explanation of turning text into representations, from back when generation wasn't the point
- [Leaving BERT Behind With DeBERTa](https://wandb.ai/akshayuppal12/DeBERTa/reports/The-Next-Generation-of-Transformers-Leaving-BERT-Behind-With-DeBERTa--VmlldzoyNDM2NTk2) - disentangled attention, explained readably. Also a good look at what incremental architecture work actually looked like

## Reasoning

Explainers first, then the actual papers. The four papers below are basically the whole story; process supervision made step-by-step correctness trainable, test-time compute gave the argument for why thinking longer beats a bigger model, GRPO made the RL cheap enough to actually run, and R1 showed you can get all of it with no supervised reasoning traces at all.

- [Understanding the New Class of "Reasoning" LLMs](https://sebastianraschka.com/blog/2025/understanding-reasoning-llms.html) - the clearest take on what actually makes a reasoning model different from a chat model
- [Demystifying Reasoning Models](https://cameronrwolfe.substack.com/p/demystifying-reasoning-models)
- [Anthropic's Research on Reasoning Models](https://www.anthropic.com/research/tracing-thoughts-language-model) - what the visible chain of thought actually corresponds to internally. Spoiler: not always what it says it is
- [Let's Verify Step by Step](https://arxiv.org/abs/2305.20050) - reward the steps, not just the final answer. Everything else builds on this
- [Scaling LLM Test-Time Compute Optimally can be More Effective than Scaling Model Parameters](https://arxiv.org/abs/2408.03314) - the scaling argument for spending compute at inference instead of training
- [DeepSeekMath](https://arxiv.org/abs/2402.03300) - where GRPO comes from. Read it before R1, and before the Cursor post above - both assume you already know what it is
- [DeepSeek-R1: Incentivizing Reasoning Capability in LLMs via Reinforcement Learning](https://arxiv.org/abs/2501.12948) - the big open result. R1-Zero gets to strong reasoning from pure RL, no supervised fine-tuning first, and the reasoning behaviours *emerge* rather than being demonstrated. Also in [Nature](https://www.nature.com/articles/s41586-025-09422-z)
- [Scaling test-time compute](https://huggingface.co/spaces/HuggingFaceH4/blogpost-scaling-test-time-compute) - HF reproducing the search side of this, with code. Moved here from the transformers section, where it never really belonged

### On AGI Timelines

- [Noam Brown on where AI researchers actually agree](https://x.com/polynoamial/status/1994439121243169176) - beyond the hype vs doom framing, most leading researchers agree the current paradigm is enough for massive impact, but a few more breakthroughs (continual learning, sample efficiency) are needed for AGI/ASI

## NLP/LLM Academic Courses

If you want to dedicate yourself to a full course in the field - here are some good options.

- [Stanford's current main NLP course](https://stanford-cs336.github.io/spring2025/)
- [Great list by Yoav Goldberg](https://gist.github.com/yoavg/95bbc5768cacd2bf07187779fada4867)

## Training Large Models: War Stories

- [OPT-175B Logbook](https://github.com/facebookresearch/metaseq/blob/main/projects/OPT/chronicles/OPT175B_Logbook.pdf) - Meta's day by day log of what it actually took to keep a 175B dense model training. The best antidote to anyone who thinks large scale training is easy

## Curated Reading Lists

Some of these are lists of lists - use them to go deeper than what's in this document.

- [a16z's AI Canon](https://a16z.com/ai-canon/) - a broad, tiered reading list from beginner explainers to deeply technical papers, covering LLMs, diffusion models and the AI market
- [Sebastian Raschka's "Understanding Large Language Models" reading list](https://sebastianraschka.com/blog/2023/llm-reading-list.html) - academic papers only, meant to be read chronologically
- Ilya Sutskever reportedly gave John Carmack this list of papers, saying "if you learn all of these, you'll know 90% of what matters today": [curated version with links to every paper](https://github.com/dzyim/ilya-sutskever-recommended-reading)

---

# Computer Vision

Vision got big enough that it lives in its own file - **[topics/computer-vision.md](topics/computer-vision.md)**.

Two threads in there. The generative one goes VAEs - GANs - diffusion - rectified flow - text-to-image personalization, roughly in the order the field figured them out. The recognition one goes AlexNet - ViT/CLIP - VLMs - video.

If you'd rather have three links than a whole file:

- [How AI Image Generators Work (Computerphile)](https://www.youtube.com/watch?v=1CIpzeNxIhU) - fifteen minutes, no maths, and correct
- [Lilian Weng's "What are Diffusion Models?"](https://lilianweng.github.io/posts/2021-07-11-diffusion-models/) - the best first technical read on DDPMs and score based models
- [Learning Transferable Visual Models From Natural Language Supervision](https://arxiv.org/abs/2103.00020) - CLIP. Made text and images share a space, and quietly enabled most of what followed
