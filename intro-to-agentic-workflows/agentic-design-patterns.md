### Four Key Design Patterns in Agentic Workflows

1\. Reflection: An LLM evaluates its own output (or receives external feedback), identifies errors, and iteratively improves the result. Example: Generate code → Review → Fix bugs → Retest.

2\. Tool Use: LLMs interact with external tools (APIs, web search, databases, code execution) to retrieve information and perform actions beyond text generation.

3\. Planning: An LLM dynamically determines the sequence of steps and tools required to accomplish a task, rather than following a hardcoded workflow.

4\. Multi-Agent Collaboration: Multiple specialized agents (e.g., Researcher, Developer, Tester) collaborate to complete complex tasks, each handling a specific responsibility.

Key Takeaways:

- These patterns can be combined to build more capable agentic workflows.
- Planning and multi-agent systems offer greater flexibility but can be harder to control.
- Evaluations (Evals) are essential for measuring performance and continuously improving workflows.
