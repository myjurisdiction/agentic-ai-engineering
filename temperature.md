# Temperature in LLMs — Explained

Temperature is a parameter that controls how random or predictable an LLM's generated response will be.

- Low temperature (0–0.3): More predictable, focused, and consistent responses.
- Medium temperature (0.4–0.7): Some flexibility and variation.
- High temperature (0.8–2): More diverse and unpredictable responses.

Temperature does not control how intelligent the model is. It controls how the model selects tokens when generating an answer.

## 1. Why do LLMs need temperature?

LLMs generate text by predicting the next token based on the preceding context.

Suppose you give an LLM this sentence:

> "I would like to drink a cup of..."

The model might assign these hypothetical probabilities:

| Next token | Probability |
| ---------- | ----------- |
| Coffee     | 70%         |
| Tea        | 20%         |
| Water      | 10%         |

Instead of always choosing "coffee," the model can sample from these probabilities.

Temperature changes the probability distribution before the next token is selected.

At low temperatures, the most likely token becomes even more dominant. At high temperatures, less likely tokens get a greater chance of being selected.

## 2. Experiment with temperature

Move the slider to see how temperature changes the next-token probabilities.

Temperature

## 0.5

0

1

2

Next-token probabilities

Focused

Coffee

90.7%

Tea

7.4%

Water

1.9%

Illustrative distribution based on the hypothetical token probabilities above. Actual LLM probabilities depend on the model and context.

Notice:

- At `temperature = 0`, the model selects the highest-probability token.
- At `temperature = 1`, the original probability distribution is preserved.
- At `temperature = 2`, the probability distribution becomes flatter, making alternative tokens more likely.

Technically, temperature rescales token logits before applying the softmax function:

\\[ P_i=\frac{e^{z_i/T}}{\sum_j e^{z_j/T}} \\]

Here, \\(z_i\\) is the model's score for token \\(i\\), and \\(T\\) is the temperature. At zero, generation typically uses greedy selection rather than this formula.

## 3. Understanding your Python code

```
response = client.chat.completions.create(    model=model,    messages=[        {"role": "user", "content": prompt}    ],    temperature=0,)
```

Here, `temperature=0` instructs a model that supports temperature sampling to favor the most probable token at each generation step.

Why would Andrew Ng use this in the chart-generation exercise?

Because you're asking an LLM to generate code for a specific task. You generally want it to follow instructions consistently rather than introduce unnecessary variation.

However, two important distinctions:

- Temperature 0 does not guarantee correctness. The most probable output can still contain mistakes.
- Temperature 0 does not guarantee identical responses across every API call. Small variations can still occur due to implementation details and model changes.

## 4. How should you use temperature in Agentic AI?

These are starting-point heuristics for models that support the parameter, not universal rules.

| Use case                  | Suggested temperature | Reason                             |
| ------------------------- | --------------------- | ---------------------------------- |
| SQL generation            | 0–0.2                 | Prefer consistent query generation |
| Code generation           | 0–0.2                 | Prefer focused implementations     |
| RAG question answering    | 0–0.3                 | Favor grounded, consistent answers |
| Reflection and evaluation | 0–0.3                 | Prefer consistent criticism        |
| General chatbot           | 0.4–0.7               | Allow some natural variation       |
| Creative writing          | 0.8–1.2               | Encourage more varied language     |

For your chart-generation reflection exercise, I would start with `temperature=0` for both generation and reflection and evaluate whether changing it improves the output.

API compatibility: OpenAI's Chat Completions documentation defines temperature on a 0–2 range, but not every model supports configuring it. In particular, newer reasoning models can reject custom temperature settings when reasoning is enabled. Check model-specific support; omit the parameter when unsupported.&#x20;

[image](https://www.google.com/s2/favicons?domain=https://platform.openai.com&sz=32)

OpenAI API Reference

+1

## 5. Temperature vs. Top-p

Both parameters influence token sampling, but differently.

- Temperature: Adjusts how strongly the model favors higher-probability tokens.
- Top-p: Restricts sampling to the smallest group of tokens whose cumulative probability reaches a specified threshold.

OpenAI generally recommends adjusting temperature or top-p rather than changing both simultaneously.&#x20;

[image](https://www.google.com/s2/favicons?domain=https://platform.openai.com&sz=32)

OpenAI API Reference

## Summary for your Agentic AI notes

Temperature is an inference-time sampling parameter that controls the randomness of token selection during LLM text generation.

- Lower temperature concentrates probability on more likely tokens, yielding more consistent outputs.
- Higher temperature flattens the distribution, encouraging more varied outputs.
- Temperature does not modify the model's weights or knowledge.
- Temperature 0 is useful for tasks requiring consistency, but it doesn't guarantee correct or reproducible outputs.
- In agentic workflows, choose temperature based on task requirements and measure quality through evaluations rather than assuming one setting is always best.

Remember: Temperature controls how the model selects its next tokens, not how deeply it reasons or whether its answer is factually correct.
