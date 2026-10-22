In Agentic AI, tools are external functions, APIs, or services that an AI agent can invoke to perform actions or retrieve information beyond what the LLM can do on its own.

Think of it this way:

- LLM (the brain): Understands the problem, reasons, and decides what needs to be done.
- Tools (the capabilities): Allow the agent to search databases, execute code, retrieve documents, call APIs, or interact with external systems.
- Agentic workflow (the orchestration): Coordinates reasoning, tool execution, and subsequent decisions to achieve a goal.

## 1. How tool calling works

Suppose you build an AI assistant that answers questions about an e-commerce order.

A user asks:

"Where is my order #1234, and when will it arrive?"

User request

Where is order #1234?

LLM decides to call a tool

getOrderStatus({ orderId: "1234" })

Tool execution by Node.js backend

Queries order database / shipping API

LLM receives the tool result

status: Shipped, ETA: October 25

Final answer

Your order has shipped and is expected to arrive on October 25.

The important distinction is that the LLM doesn't execute your JavaScript function itself. It generates a structured tool-call request. Your Node.js application executes the function and returns the result to the LLM.

## 2. Common types of tools in Agentic AI

| Tool category         | Example                         | Purpose                            |
| --------------------- | ------------------------------- | ---------------------------------- |
| Information retrieval | Web search                      | Retrieve up-to-date information    |
| Database              | PostgreSQL query                | Fetch structured business data     |
| Code execution        | Python/JavaScript sandbox       | Execute code and analyze data      |
| RAG retrieval         | `searchDocuments()`             | Retrieve relevant document chunks  |
| External APIs         | GitHub, Slack, Jira             | Interact with external services    |
| Action tools          | `sendEmail()`, `createTicket()` | Perform real-world operations      |
| Memory                | `getUserPreferences()`          | Retrieve previously stored context |

## 3. How do we define a tool in Node.js?

Suppose you implement a document search tool for your RAG application.

First, you create a normal JavaScript function:

```
async function searchDocuments(query) {
  const results = await vectorDatabase.search(query);
  return results;
}
```

Next, you describe that function to the LLM using a tool definition.

Conceptually:

```
const tool = {
  name: "searchDocuments",
  description: "Search uploaded documents for relevant information",
  parameters: {
    query: "string"
  }
};
```

This is a simplified illustration. Actual SDKs typically require a JSON Schema for the parameters.

When the user asks a question, the model may generate a tool call such as:

```
{
  name: "searchDocuments",
  arguments: {
    query: "What are the adverse effects of Drug X?"
  }
}
```

Your backend then performs the requested operation, validates its arguments, and returns the retrieved information.

The LLM uses that information to generate a grounded response.

## 4. Tool calling vs. Agentic AI

This is an important distinction for interviews.

Tool calling is a capability, while Agentic AI is a broader workflow.

A conventional LLM application might make one predetermined tool call.

An agent can dynamically decide:

1. Whether a tool is necessary.
2. Which available tool to call.
3. What arguments to supply.
4. Whether another tool call is needed after inspecting the result.
5. When it has enough information to respond.

For example, an agent may call `searchDocuments()`, discover missing information, call `webSearch()`, and then synthesize the results.

However, simply calling multiple tools doesn't automatically make a system autonomous. The degree of agency depends on how much planning and decision-making control you give the model.

## 5. How tools relate to other Agentic AI patterns

| Concept     | Meaning                                            |
| ----------- | -------------------------------------------------- |
| Tool use    | Agent interacts with external systems              |
| Reflection  | Agent evaluates and improves its previous output   |
| Planning    | Agent decomposes a complex task into smaller steps |
| Multi-agent | Multiple specialized agents collaborate            |

These patterns can be combined. For example, an agent can plan a task, execute tools, reflect on their results, and retry when necessary.

For your Node.js RAG project, start with a single `searchDocuments` tool, implement the tool-calling loop, and add additional tools only when necessary.

One particularly important concept to study next is the agent execution loop: how the model requests a tool, how your backend executes it, how the result is fed back into the model, and how the cycle repeats until the agent produces its final answer.
