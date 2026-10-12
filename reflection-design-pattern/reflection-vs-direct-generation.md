### Reflection vs. Direct Generation

- Direct Generation: An LLM generates an answer in a single attempt without reviewing or improving it.
- Prompting Techniques:
  - Zero-shot: No examples provided in the prompt.
  - One-shot: One input-output example provided.
  - Few-shot: Multiple examples provided.
- Reflection: An LLM reviews its initial output, identifies errors, and generates an improved version. Research shows reflection often improves performance over direct generation.
- Use Cases: Validating complex JSON/HTML structures, checking instructions for completeness, reviewing emails, and evaluating generated content.
- Effective Reflection Prompts: Explicitly ask the LLM to review its output against specific criteria (e.g., correctness, completeness, tone, factual accuracy) before revising it.

Key Takeaway: Reflection can improve output quality compared with direct generation, especially when guided by clear evaluation criteria. However, its effectiveness depends on the task and model.

Workflow: Generate → Review Against Criteria → Identify Errors → Revise.
