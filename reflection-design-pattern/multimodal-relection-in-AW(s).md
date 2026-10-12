### Multimodal Reflection in Agentic Workflows

- Multimodal Reflection: Uses multimodal LLMs to evaluate outputs such as images, charts, or diagrams and suggest improvements through visual reasoning.
- Workflow: Generate Python code → Execute code → Generate chart → Analyze chart using a multimodal LLM → Critique → Improve code → Regenerate chart.
- External Feedback: Providing both the generated code and its visual output helps the LLM identify issues that code inspection alone might miss.
- Model Selection: Different models can handle generation and reflection. Reasoning models may perform better at identifying issues.
- Effective Reflection Prompts: Specify clear evaluation criteria such as readability, clarity, accuracy, and completeness.
- Evaluate Effectiveness: Reflection doesn't always improve results. Use evals to measure whether it improves your application's output quality.

Key Takeaway: Multimodal reflection enables agents to inspect and improve visual outputs, but its effectiveness should be measured rather than assumed.
