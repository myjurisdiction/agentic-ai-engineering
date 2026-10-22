# Evaluating Reflection in Agentic AI Workflows

## 1. Why do we need evaluations (Evals)?

Reflection can improve an LLM's output by reviewing and refining its initial response. However, it introduces additional latency and computational cost.

Before introducing reflection into an agentic workflow, we should measure whether the improvement justifies the overhead.

Evals help us:

- Measure whether reflection actually improves output quality.
- Compare performance with and without reflection.
- Experiment with different generation and reflection prompts.
- Systematically optimize agentic workflows rather than relying on intuition.

## 2. Evaluating reflection using objective metrics

Example: LLM-generated SQL queries

Suppose a user asks: "Which product color has the highest total sales?"

Without reflection

User Question → LLM Generates SQL → Execute Query → Answer

With reflection

User Question → Generate SQL → Reflect & Improve SQL → Execute Query → Answer

How to evaluate:

1. Prepare a dataset of 10–15 questions with known correct answers (ground truth).
2. Run each question through both workflows.
3. Compare their final answers against the ground truth.
4. Calculate the percentage of correct answers.

Without reflection

# 87%

Accuracy

With reflection

# 95%

Accuracy

In the course's illustrative example, reflection produces an 8-percentage-point improvement in accuracy.

This is an example of objective evaluation, because the generated answer can be checked against a known correct answer.

## 3. Evaluating subjective outputs using LLM-as-a-Judge

Some AI-generated outputs cannot be evaluated using simple right-or-wrong criteria.

Examples include data visualizations, written content, and UI designs.

One approach is LLM-as-a-Judge, where another LLM evaluates the quality of the generated output.

However, directly asking an LLM to compare two outputs can be unreliable because:

- Position bias: The model may favor the first option regardless of quality.
- Prompt sensitivity: Small changes in evaluation instructions can produce different judgments.
- Poor calibration: Ratings may not correspond consistently to expert human judgments.

### Better approach: Rubric-based evaluation

Instead of asking an LLM to rate a visualization from 1 to 5, provide explicit binary criteria (0 or 1).

For example:

Example visualization rubric

Illustrative

Does the chart have a clear title?

01

Are the axes correctly labeled?

01

Is the selected chart type appropriate?

01

Is the information easy to understand?

01

Are colors and legends used appropriately?

01

Total quality score

# 3 / 5

Try changing the binary scores to see how rubric-based grading works.

The LLM evaluates each criterion independently, and the scores are added together.

Why is this better? Binary criteria are more concrete than arbitrary numerical ratings, making evaluations generally more consistent and interpretable.

## 4. Code-based Evals vs. LLM-as-a-Judge

| Aspect          | Code-based Evals             | LLM-as-a-Judge                   |
| --------------- | ---------------------------- | -------------------------------- |
| Best suited for | Objective tasks              | Subjective tasks                 |
| Examples        | SQL answers, calculations    | Charts, writing, design          |
| Evaluation      | Compare against ground truth | Grade against a rubric           |
| Consistency     | Usually high                 | Depends on rubric and model      |
| Complexity      | Generally simpler            | Requires calibration and testing |

Rule of thumb: Prefer code-based evaluation when a correct answer can be verified programmatically. Use LLM-as-a-Judge when quality requires subjective judgment, ideally with a clearly defined rubric.

## 5. Evals enable systematic prompt optimization

Once an evaluation dataset is established, we can experiment with:

- Different initial generation prompts.
- Different reflection prompts.
- Additional reflection instructions, such as improving SQL performance or readability.
- Alternative agentic workflows.

After each modification, rerun the same evaluation dataset to measure whether performance improves.

This creates a repeatable optimization process:

Generate → Evaluate → Modify Prompts → Re-evaluate → Compare Results

For reliable comparisons, keep the dataset and scoring criteria consistent between experiments.

## Key takeaways for interviews

1. Reflection is not automatically beneficial. Measure the accuracy improvement against its added latency and cost.
2. Evals quantify workflow quality. Use representative test cases and ground-truth answers whenever possible.
3. Objective vs. subjective evaluations: Use programmatic checks for objectively verifiable outputs and LLM-as-a-Judge for subjective quality.
4. Rubric-based grading is preferable to vague ratings. Multiple binary criteria generally produce more consistent judgments.
5. LLM judges have limitations, including position bias, prompt sensitivity, and disagreement with human experts.
6. Evals are essential for iterative improvement. They allow developers to compare prompts, reflection strategies, and agentic workflow designs systematically.

Core principle: Don't add reflection simply because it seems to produce better answers. Build evaluations to establish whether it measurably improves the system enough to justify the additional cost and latency.
