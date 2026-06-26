# 20 AI Terms Every Engineer Should Know

**Source:** https://www.youtube.com/watch?v=OYvlznJ4IZQ  
**Channel:** GKCS

## TL;DR
A practical glossary of 20 foundational AI/LLM terms — from tokenization and attention to RAG, MCP, agents, and quantization — aimed at engineers who build or communicate about AI systems.

## Key Points

**Core LLM Concepts**
- **Large Language Model (LLM)** — a neural network trained to predict the next token of an input sequence
- **Tokenization** — breaking input text into discrete tokens (not just by spaces; suffixes like *-ers*, *-ing* carry meaning); essential for the model to understand natural language structure
- **Vectors / Vectorization** — mapping words to coordinates in an n-dimensional space so that semantically similar words cluster together; this is how LLMs encode meaning
- **Attention (2017)** — mechanism that resolves ambiguous words (e.g. "apple") by looking at nearby contextual words and pushing the word's vector toward the correct meaning; made famous with GPT-2 in 2022
- **Self-supervised learning** — training without human labels by masking parts of existing text and predicting them; makes data collection massively scalable and is now adopted even by image/video models

**Architecture & Training**
- **Transformer** — the specific algorithm inside most LLMs: input tokens → attention block → feedforward network, stacked 12–100s of layers; separate from the concept of an LLM itself (the LLM is the product, transformer is the engine)
- **Fine-tuning** — after base model training, run it through domain-specific Q&A pairs to update weights; penalizes plausible-but-undesirable responses; same base model can produce multiple fine-tuned variants (e.g. medical, financial)

**Inference-Time Techniques**
- **Few-shot prompting** — augmenting the user query with worked examples at inference time so the model sees the expected response format before generating
- **RAG (Retrieval Augmented Generation)** — server fetches relevant documents (policy docs, T&Cs) from a vector DB at query time and appends them to the prompt alongside examples; dramatically improves response quality for company-specific context
- **Vector Database** — stores documents as vectors; uses similarity search (e.g. HNSW algorithm) to find documents closest to an incoming query; common choices include Neo4j (graph DB) and Neon (vector DB)
- **MCP (Model Context Protocol)** — protocol that lets an LLM client connect to external MCP servers (e.g. airline APIs) at runtime, retrieve real-time data, and even trigger actions (e.g. book a flight) — not just read data
- **Context Engineering** — umbrella term covering few-shot prompting + RAG + MCP + user preference tracking + prompt/context summarization (e.g. sliding window of last 100 chats + summary of older history); stateful, evolves per user vs. stateless prompt engineering

**Agents & Learning**
- **Agents** — long-running server processes that can query LLMs, external systems, and other agents autonomously; act on opportunities (e.g. cheap flights) based on user preferences without human intervention per step
- **RLHF (Reinforcement Learning with Human Feedback)** — human selects the better of two model responses (+1 / -1); over many examples this builds a vector space of "good" vs "bad" paths, training the model to follow high-scoring paths (analogous to Pavlov's dog)
- **Chain of Thought** — training/prompting the model to reason step by step; harder problems trigger more steps (seen in DeepSeek); improves response quality significantly over direct answers
- **Reasoning Models (LRMs)** — models trained to figure out *how* to solve a problem step by step; can use tree-of-thought, graph-of-thought, or tool use; examples: DeepSeek, OpenAI o1/o3

**Model Variants**
- **Multimodal Models** — accept/generate images and video in addition to text; performance is often better than text-only models because visual training deepens semantic understanding
- **Small Language Models (SLMs)** — 3M–300M parameters (vs 3B–300B for LLMs); trained on company- or task-specific proprietary data; faster and cheaper to run; trade general capability for domain precision
- **Distillation** — a large "teacher" LLM and a small "student" SLM receive the same input; student learns to mimic teacher's output; student weights update only when outputs diverge; condenses knowledge into a fraction of the memory footprint
- **Quantization** — compresses trained model weights from 32-bit to 8-bit (saving ~75% memory); applied *after* training (does not reduce training cost); reduces inference/production hosting cost

## Notable Quotes
- "The large language model is actually the product. You can think of it as a car. And the transformer is the engine."
- "Prompt engineering is stateless. Context engineering evolves as per the user's declared preferences and previous chat history."
- "Reinforcement learning cannot build mental models — it can just tell you based on outcomes what is more likely and what is a more beneficial path."

## Action Items / Takeaways
- Use RAG + MCP together for production AI apps that need both internal company context and live external data
- Prefer SLMs + distillation when cost, latency, or data privacy matter more than general capability
- Apply quantization post-training to cut inference costs without re-training
- Distinguish *prompt engineering* (stateless, one prompt) from *context engineering* (stateful, evolves with the user)
- Check GKCS's detailed videos on MCP and Agents for deeper dives on those two topics
