# Skills vs Tools in Agentic AI

These two terms are often used interchangeably, but they have distinct meanings in agentic AI systems.

---

## 🔧 Tools

**Tools** are low-level, atomic capabilities that an agent can invoke to interact with external systems or perform discrete actions.

| Characteristic | Description |
|---|---|
| **Scope** | Single, well-defined operation |
| **Examples** | `web_search()`, `read_file()`, `execute_code()`, `call_api()` |
| **Invocation** | Direct function/API call |
| **Statefulness** | Typically stateless |
| **Composability** | Building blocks for higher-level logic |

---

## 🧠 Skills

**Skills** are higher-level, reusable capabilities that often **orchestrate multiple tools** to accomplish a more complex goal.

| Characteristic | Description |
|---|---|
| **Scope** | Multi-step, goal-oriented behavior |
| **Examples** | `ReviewPullRequest`, `DebugStackTrace`, `SummarizeRepository` |
| **Invocation** | May involve reasoning, planning, and tool chaining |
| **Statefulness** | Often stateful across multiple steps |
| **Composability** | Can compose other skills AND tools |

---

## Key Distinctions

```
Tools:   search_web("query")    ──►  returns raw results
                                          │
Skills:  ResearchTopic("query") ──►  plans → calls search_web()
                                           → synthesizes results
                                           → formats response
```

| Dimension | Tools | Skills |
|---|---|---|
| **Granularity** | Fine-grained | Coarse-grained |
| **Intelligence** | None (deterministic) | Embedded reasoning/planning |
| **Reusability** | Low-level reuse | High-level reuse |
| **Definition** | Function signatures | Instruction sets / prompt templates |
| **Failure handling** | Errors bubble up | Can self-correct and retry |

---

## In Practice

- **Tools** are typically defined as **function schemas** (e.g., OpenAI function calling, MCP tool definitions).
- **Skills** are typically defined as **instruction sets**, **prompt templates**, or **sub-agents** that know *when and how* to use tools.
- A single skill may invoke **many tools** in sequence or in parallel.
- Skills encode **domain expertise**; tools encode **system access**.

---

## Example: "Review a Pull Request"

```
Skill: ReviewPullRequest
  └─► Tool: get_pull_request_diff()
  └─► Tool: search_code("related functions")
  └─► Tool: get_ci_status()
  └─► Tool: post_review_comment()
  [+ reasoning about code quality, security, etc.]
```

The **skill** knows *what to do*. The **tools** know *how to do one thing*. Together, they enable capable agentic behavior.
