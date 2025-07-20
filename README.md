# An Always*-Updating List of LLM Resources

**when I feel like it*

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

---

## Technical and Science Stuff

## Understanding Transformers and Attention
### Karpathy's "Building GPT From Scratch"

If you are going to find the time for just one resource, this is by far the best and most
intuitive resources. As always with *Andrej Karpathy* - he is the master of explaining complex topics in Machine Learning related maths/engineering.

- [Karpathy's minimal GPT repo](https://github.com/karpathy/minGPT)
- [Let's build GPT: from scratch, in code, spelled out](https://www.youtube.com/watch?v=kCc8FmEb1nY)
- [Let's reproduce GPT-2 (124M)](https://www.youtube.com/watch?v=l8pRSuU81PU)

### Other Good Resources
- [The Annotated Transformer](https://nlp.seas.harvard.edu/annotated-transformer/)
- [Really deep dive into transformer inference arithmetic](https://kipp.ly/transformer-inference-arithmetic/#kv-cache)
- [Getting Meaning From Text: Self-Attention Step-by-Step](https://pub.towardsai.net/getting-meaning-from-text-self-attention-step-by-step-video-7d8f49694f89)
- [GPT in 60 Lines of NumPy](https://jaykmody.com/blog/gpt-from-scratch/)
- [Becoming the Unbeatable: How I Fine-Tuned GPT's KV Cache](https://dipkumar.dev/becoming-the-unbeatable/posts/gpt-kvcache/)
- [HG's Test Time Compute](https://huggingface.co/spaces/HuggingFaceH4/blogpost-scaling-test-time-compute)


### Courses
If you want to dedicate yourself to a full course in the field - here are some good options.
- [Stanford's current main NLP course](https://stanford-cs336.github.io/spring2025/)
- [Great list by Yoav Goldberg](https://gist.github.com/yoavg/95bbc5768cacd2bf07187779fada4867)

## Retrieval and RAG

- [Anthropic's blogpost on contextual retrieval](https://www.anthropic.com/news/contextual-retrieval) - this is an important resource!
- [Pinecone's comprehensive guide to vector indexes](https://www.pinecone.io/learn/series/faiss/vector-indexes/)
- [Pinecone on HNSW specifically](https://www.pinecone.io/learn/series/faiss/hnsw/)
- [Okapi BM25](https://en.wikipedia.org/wiki/Okapi_BM25)
- [Pinecone's take on rerankers](https://www.pinecone.io/learn/series/rag/rerankers/)

## Knowledge Graphs

## Agents


## Using LLMs

### CoT
- Original Paper: [Chain-of-Thought Prompting Elicits Reasoning in Large Language Models](https://arxiv.org/abs/2201.11903)
- [Google Research blog on chain of thought](https://research.google/blog/language-models-perform-reasoning-via-chain-of-thought/)
- [Anthropic's practical guide to chain of thought](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/chain-of-thought)
- [Anthropic on chain prompts](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/chain-prompts)

## Reasoning

- [Anthropic's Research on Reasoning Models](https://www.anthropic.com/research/tracing-thoughts-language-model)
- [Demystifying Reasoning Models](https://cameronrwolfe.substack.com/p/demystifying-reasoning-models)
- [Understanding the New Class of "Reasoning" LLMs](https://sebastianraschka.com/blog/2025/understanding-reasoning-llms.html)


## MCP/Cursor

- [cursor-mcp-examples](https://github.com/nirbenz/cursor-mcp-examples) (this was written by me)
- [Cursor's docs on tools](https://docs.cursor.com/tools)
- [Cursor's docs on rules](https://docs.cursor.com/context/rules)
- [Cursor Custom Agents Rules Generator](https://github.com/bmadcode/cursor-custom-agents-rules-generator)
- [Big collection of cursor rules](https://github.com/PatrickJS/awesome-cursorrules)
- [GitHub's MCP server](https://github.com/github/github-mcp-server)
- [Model Context Protocol Python SDK](https://github.com/modelcontextprotocol/python-sdk)
- [Linear's MCP Integration Announcement](https://linear.app/changelog/2025-05-01-mcp)