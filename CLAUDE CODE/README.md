# SUMMARY

## CLAUDE-CODE CLI
```go
npm install -g @anthropic-ai/claude-code
```

## MemPalace - Memory Manager
```go
claude plugin marketplace add milla-jovovich/mempalace
claude plugin install --scope user mempalace
```

This referre of this project: [MemPalace](https://github.com/milla-jovovich/mempalace)

## .claude settings.json
These config bellow aims to improve and reduce the token usage on Claude Code.
```json
{
    "env": {
      "MAX_THINKING_TOKENS": "32000",
      "CLAUDE_AUTOCOMPACT_PCT_OVERRIDE": "65",
      "CLAUDE_CODE_SUBAGENT_MODEL": "sonnet"
    },
    "model": "sonnet",
    "effortLevel": "medium"
}
```
