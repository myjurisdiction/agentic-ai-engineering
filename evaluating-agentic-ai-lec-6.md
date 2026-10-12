### Evaluations (Evals) in Agentic Workflows

- Purpose: Evals measure an agent's performance, identify errors, and guide iterative improvements.
- Build First, Evaluate Next: Start with a working agent, manually inspect outputs, identify weaknesses, and then define evaluation metrics.
- Objective Evals: Use code to measure quantifiable errors (e.g., how often an agent mentions competitors).
- Subjective Evals (LLM as Judge): Use another LLM to evaluate output quality, such as accuracy, relevance, or coherence.
- Types of Evals:
  - End-to-End Evals: Evaluate the final output of the entire workflow.
  - Component-Level Evals: Evaluate individual steps within the workflow.
- Error Analysis: Inspect intermediate outputs (traces) to identify which steps are causing problems.

Key Takeaway: Build → Inspect Outputs → Identify Errors → Define Evals → Improve → Repeat.

Evals help transform agent development from trial and error into a measurable, systematic improvement process.