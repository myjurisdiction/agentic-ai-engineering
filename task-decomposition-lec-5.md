### Task Decomposition in Agentic Workflows — Key Takeaways

\- 1. Break complex tasks into smaller steps: Instead of asking an LLM to perform a complex task in one go, decompose it into discrete, manageable steps, similar to how a human would approach the problem.

\- 2. Evaluate each step for feasibility: Ask yourself: Can this step be performed by an LLM, a function call, an API, or another software tool? If not, break it down further.

\- 3. Combine different building blocks: Agentic workflows typically use:

- LLMs: Reasoning, generating content, extracting information, making decisions.
- Tools/APIs: Web search, database queries, sending emails, retrieving external data.
- Specialized AI models: PDF processing, image analysis, speech recognition.
- Code execution: Writing and executing code to accomplish tasks.

\- 4. Example — Research Agent:

- Initial workflow: Generate outline → Search web → Write essay.
- Improved workflow: Generate outline → Search web → Write first draft → Critique draft → Revise draft.
- Lesson: Adding reflection and revision steps can improve output quality and consistency.

\- 5. Other examples of task decomposition:

- Customer support: Extract email details → Query customer database → Generate and send response.
- Invoice processing: Extract invoice information → Validate information → Save to database.

\- 6. Iterate and refine workflows: Your first agentic workflow rarely produces the best results. Evaluate its performance, identify weak steps, and further decompose or improve them.

\- 7. Evaluations (Evals) are essential: Establish ways to measure workflow quality so you can systematically improve accuracy, reliability, and overall performance.

Core Principle: Task Decomposition → Identify LLM/Tool Capabilities → Build Workflow → Evaluate Results → Refine and Iterate.

The key skill in agentic AI engineering isn't just prompting an LLM — it's designing an effective sequence of LLM reasoning steps and tool executions to solve complex problems reliably.