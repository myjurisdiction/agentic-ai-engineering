### Reflection Design Pattern in Agentic AI

- Reflection: An LLM reviews its own output, identifies mistakes, and generates an improved version.
- Workflow: Generate initial output (V1) → Reflect/Critique → Improve output (V2).
- Model Selection: The same LLM or a different model (e.g., a reasoning model for detecting code bugs) can perform the reflection step.
- External Feedback: Reflection becomes significantly more effective when provided with additional information, such as code execution results, test failures, or error logs.
- Iterative Improvement: Reflection can be repeated to improve output quality, although it doesn't guarantee perfect results.

Key Takeaway: Reflection is most powerful when combined with external feedback rather than relying solely on an LLM's self-critique.
