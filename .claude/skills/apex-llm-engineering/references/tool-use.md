# Tool Use

## Scope
Function calling: defining tools the model can invoke, schema design, execution, error handling, and the tool-result loop.

## Core principles
- The tool description is a prompt, not documentation: the model chooses and fills tools based entirely on name, description, and parameter schemas — write them for the model (when to use, when not to, what it returns, example values), and eval them like prompts.
- Design tools around intent, not endpoints: one `search_orders(query, status, date_range)` beats five thin CRUD wrappers; every extra tool and parameter is another decision the model can get wrong.
- Tool results are attacker-controlled input when they carry external content (web pages, emails, tickets): a tool-using model is an injection surface, so treat results as data, sanitize/delimit them, and never grant write-tools on the basis of read-content instructions.
- Errors must return to the model as structured, actionable text ("date must be YYYY-MM-DD, got '3/4/24'") — an opaque 500 teaches the model nothing, a good error message lets it self-correct in one turn.
- Enforce schemas mechanically, not hopefully: validate arguments server-side (types, enums, ranges, authz) before execution; the model's output is a suggestion, your validator is the contract.

## Apex practices
- Keep tool results compact and relevant: return the 5 fields the task needs, not the 200-field raw API response — bloated results burn context and bury the signal the model must act on.
- Use enums and constrained types in JSON Schema wherever possible; `"status": {"enum": ["open","closed"]}` eliminates a whole class of invented values.
- Support and test parallel tool calls for independent operations (fetching three records at once), but serialize dependent ones; document dependencies in descriptions ("call lookup_customer before create_ticket").
- Build a tool-level test suite: golden prompts → expected tool + arguments, run on every prompt or schema change; tool-selection regressions are silent and common.

## Pitfalls
- Dumping an entire OpenAPI spec as the toolset — 60 auto-generated tools with parameter soup reliably underperform 8 hand-designed ones.
- Letting the model pass through freeform strings to shells, SQL, or eval-like sinks; parameterize and allowlist, exactly as you would for any untrusted caller.
- Ignoring the "no tool" case: models over-call tools when one seems relevant; explicitly describe when to answer directly, and eval for spurious calls.

## Tools & references
Anthropic tool-use docs and "Writing effective tools for agents", OpenAI function calling guide, JSON Schema, Berkeley Function-Calling Leaderboard (BFCL), MCP for standardized tool servers.
