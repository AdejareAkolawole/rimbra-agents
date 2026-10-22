# Rimbra for Claude Code

Connects Claude Code to your [Rimbra](https://rimbra.app) workspace and teaches it how Rimbra works.

```
/plugin marketplace add AdejareAkolawole/rimbra-agents
/plugin install rimbra@rimbra
```

The first time Claude uses Rimbra, run `/mcp` and sign in. Pick the workspace and whether Claude may deploy (Developer) or only read (Viewer).

Prefer a key? Make one in Rimbra → MCP and run:

```
claude mcp add --transport http rimbra https://app.rimbra.app/mcp --header "Authorization: Bearer YOUR_KEY"
```

Docs: https://app.rimbra.app/docs/mcp
