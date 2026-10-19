
# AMA Q & A

## 1. What is compaction?

**Answer:**

Compaction is the process of summarizing or compressing a conversation when its context becomes too large,    
so the model can continue working without retaining every previous message in full.

Compaction happens automatically and can be done mannually.

---

## 2. What is AI Fluency?

**Answer:**

AI Fluency is the ability to use AI systems effectively, responsibly, and critically to achieve a goal.

It involves understanding what AI can do, communicating instructions clearly,   
evaluating AI-generated outputs, and taking responsibility for the final results.

Important aspects include:

- **Effective communication:** Giving clear instructions and useful context.
- **Critical evaluation:** Checking AI-generated answers for errors and bias.
- **Responsible use:** Considering privacy, safety, fairness, and ethical implications.
- **Human-AI collaboration:** Knowing when to use AI and when human judgment is necessary.

---

## 3. What is MCP Inspector?

**Answer:**

MCP Inspector is an interactive developer tool used to inspect, test, and debug Model Context Protocol (MCP) servers.
MCP is a protocol that allows AI applications to connect to external tools and data sources through a standardized interface.
MCP Inspector helps developers:

- Connect to an MCP server.
- Inspect available tools, resources, and prompts.
- View tool input schemas.
- Invoke tools with test arguments.
- Inspect responses and diagnose connection or protocol issues.


---

## 4. What is the `CLAUDE.md` file?

**Answer:**

`CLAUDE.md` is a Markdown file used by Claude Code to provide persistent instructions and project-specific context.

Claude Code can load applicable `CLAUDE.md` files and use their instructions when working on a project.

These files can describe:

- Project architecture and directory structure.
- Coding conventions and naming rules.
- Commands for installing dependencies and running tests.
- Important implementation decisions.
- Project-specific constraints and workflows.

---

## 5. What is a context window?

**Answer:**

A context window is the maximum amount of information a model can process as context for a particular request or generation.

It is measured in tokens, not words or characters.

Depending on the model and API, the context can include:

- System instructions.
- Developer instructions.
- Conversation history.
- User messages.
- Tool calls and tool results.
- Relevant code and documents.
- Other content supplied to the model.

The model's output also has token limits, which are related to but distinct from the context-window limit.

---
