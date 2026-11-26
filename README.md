# Tofu plugins for AI assistants

Connect Claude Code to your Tofu Field Service account and ask about invoices, estimates, clients, jobs and schedule. The plugin reads the business you choose when connecting. It cannot create or change records, send invoices or reminders, or take payments.

## Repository layout

| Path | Content |
|---|---|
| `.claude-plugin/marketplace.json` | Claude Code marketplace `tofu-plugins` |
| `plugins/claude/` | Claude Code plugin `tofu-field-service`: manifest, MCP connection, five skills and documentation |

Client packages live under `plugins/<client>/`. The next package can use `plugins/openai/`; it is not included yet. Each client package keeps its own manifest and connection configuration. The Claude marketplace lists only `plugins/claude/`.

## Install in Claude Code

```bash
claude plugin marketplace add GetPaid-Inc/Tofu.Ai.Plugins.Public
claude plugin install tofu-field-service@tofu-plugins
```

Run `/mcp`, choose `plugin:tofu-field-service:tofu`, sign in with your Tofu account and select the business to connect.

See the [Claude plugin README](plugins/claude/README.md) for skills, data access and disconnect instructions.

## Try a local checkout

From the repository root:

```bash
claude --plugin-dir ./plugins/claude
```

The plugin uses the Tofu MCP server at `https://api.tofu.com/mcp`. Installing the package and authorizing access to a Tofu business are separate steps.

## Validate

```bash
claude plugin validate --strict .
claude plugin validate --strict ./plugins/claude
claude plugin validate --strict --profile directory ./plugins/claude
```

The directory profile checks additional publication requirements. Local validation does not replace the directory's security scan and review.

## License

Apache License 2.0, see [LICENSE](LICENSE). Copyright GetPaid Inc.
