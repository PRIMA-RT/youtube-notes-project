# RNNs and LSTMs Explained

**Source:** https://www.youtube.com/watch?v=JgHQS9SED4o

## TL;DR
Plain networks can't handle sequences because order matters; Recurrent Neural Networks (RNNs) solve this with a memory loop, and LSTMs fix RNNs' tendency to forget long-range context using a gated "conveyor belt" cell state.

## Key Points

**Why Sequences Need Special Treatment**
- "Dog bites man" vs "man bites dog" — same words, opposite meanings; order carries meaning
- Plain networks see a "bag of inputs" with no sense of before/after — fatal for sequences

**Recurrent Neural Networks (RNNs)**
- Core idea: a single loop — process one element at a time, pass a summary (hidden state) back into itself at each step
- Unrolled across time: same cell, same weights, copied once per step — it's one network applied repeatedly
- Hidden state = running memory vector updated at every step, giving accumulated context at prediction time

**The Vanishing Gradient Problem**
- In practice, plain RNNs forget: signals fade as they pass through many steps (repeated multiplications)
- Same vanishing gradient problem from backprop, but stretched across time
- Long sentences = early words wash out = short effective memory

**LSTM — Long Short-Term Memory**
- Adds a second pathway: a **cell state** running straight along the top like a conveyor belt
- Information can travel along it almost untouched, giving it a protected lane
- Controlled by three learnable gates (each a tiny neural network, output 0–1):
  - **Forget gate** — what to erase from memory
  - **Input gate** — what new information to write
  - **Output gate** — what to read out right now
- Manages memory deliberately instead of by accident

**GRU — Gated Recurrent Unit**
- Streamlined LSTM: merges gates down to two, drops the separate cell state
- Faster to train with often similar results; same core idea, fewer moving parts

**Applications of Gated RNNs**
- Machine translation (word by word)
- Speech recognition and text generation
- Time series forecasting (weather, demand, markets)
- Were state of the art for sequences for years

**Fundamental Limitation of RNNs**
- Strictly sequential: can't compute step 50 until step 49 is done
- Sequential bottleneck is painfully slow on modern parallel hardware (GPUs)
- Even LSTMs struggle over very long range (e.g., linking a pronoun to a name paragraphs earlier)

## Notable Quotes
- "Dog bites man and man bites dog use the exact same words, but mean completely different things. The order carries the meaning."
- "Instead of forcing every memory through a mangling transformation, the LSTM gives it a protected lane to travel down."
- "Learnable valves that manage memory deliberately instead of by accident."

## Action Items / Takeaways
- When working with sequential data (text, audio, time series), understand that plain networks lose ordering information
- Prefer LSTMs over vanilla RNNs for tasks with long-range dependencies
- Consider GRUs when training speed matters and the task doesn't require ultra-long memory
- Know that RNNs/LSTMs have been largely replaced by **Attention-based Transformers** — the video teases this as the next topic
