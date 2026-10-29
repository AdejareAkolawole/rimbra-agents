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

Docs: https://rimbra.app/docs/mcp

## What is Rimbra?

[Rimbra](https://rimbra.app) puts a product on the internet from one account: [app hosting from GitHub](https://rimbra.app/products/deploy), [managed PostgreSQL, MySQL and Redis](https://rimbra.app/products/databases), [domains with automatic HTTPS](https://rimbra.app/products/domains), an [Email API](https://rimbra.app/products/email-api) and [Social notifications](https://rimbra.app/products/whatsapp-api) for WhatsApp messages. One dashboard, one bill, and a [free plan](https://rimbra.app/pricing) to start.

- Website: https://rimbra.app
- Docs: https://rimbra.app/docs
- Changelog: https://rimbra.app/changelog
