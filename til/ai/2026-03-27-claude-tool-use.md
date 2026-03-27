# Claude tool_use Parameter Structure

**Date:** 2026-03-27  
**Category:** AI / Prompting  
**Source:** Anthropic docs + experimentation

---

## What I Learned

When building agents with the Claude API, the `tools` parameter expects a specific structure that differs slightly from OpenAI's function calling format.

### Key Structure

```json
{
  "name": "tool_name",
  "description": "What this tool does — be specific, Claude reads this",
  "input_schema": {
    "type": "object",
    "properties": {
      "param": { "type": "string", "description": "..." }
    },
    "required": ["param"]
  }
}
```

### Key Insight

Claude uses the `description` field heavily to decide *when* to call a tool. A vague description = wrong tool calls. A specific description = reliable behavior.

### Example

Bad: `"description": "Gets weather"`  
Good: `"description": "Get current weather conditions and 5-day forecast for a specific city. Use when user asks about weather, temperature, or climate for a location."`

---

## References

- [Anthropic Tool Use Docs](https://docs.anthropic.com/en/docs/tool-use)
