## Multi-Adapter LLM with vLLM

This project demonstrates a simple system for serving multiple LoRA adapters (code generation and summarization) on top of a single base LLM using vLLM.

---

### Overview

- **Base Model:** TinyLlama-1.1B  
- **Serving Engine:** vLLM  
- **Adapters:**
  - Code Assistant (programming tasks)
  - Summarizer (concept explanations)
- **Router:** Automatically selects adapter based on prompt  

---

### How it works
User Prompt → Router → Adapter → vLLM → Response


- Prompts are routed to the appropriate adapter  
- All adapters share the same base model  
- Inference is handled through a single vLLM instance  

---

### Features

- Multi-adapter inference on one model  
- Automatic task routing (code vs summarization)  
- Performance benchmarking (~35 tokens/sec)  
- Adapter switching analysis  
- Qualitative output evaluation  

---

### Example Outputs

**Prompt:** Write a Python function for longest common subsequence  
→ Routed to: Code Assistant  

```python
def longest_common_subsequence(s1, s2):
    # dynamic programming approach
    ...
```

Prompt: Explain transformer architecture
→ Routed to: Summarizer

Uses self-attention to model relationships between tokens
Employs multi-head attention for parallel context learning
Uses positional encoding to retain sequence order

---

### Benchmark Summary
- Avg latency: ~5.1s
- Throughput: ~35 tokens/sec
- Code tasks: ~6.5s (longer outputs)
- Summarization: ~3.7s

Key Insight:
Latency is primarily driven by output length, not model speed.

### Evaluation & Observations

- Code adapter produces more structured but longer outputs  
- Summarizer is faster but can be less precise  
- Routing works well for explicit prompts  
- Performance drops on ambiguous queries  

---

### Failure Cases

- Misinterpretation of prompts (e.g., “Attention Is All You Need”)  
- Incorrect or incomplete code generation despite fluent responses  

---

### Future Improvements

- Smarter routing (ML-based classifier)  
- Better fine-tuning datasets  
- Add simple UI (Gradio / Streamlit)  
- Add quantitative evaluation metrics  
