# Claude Code Plugin Marketplace

A curated collection of plugins for [Claude Code](https://claude.ai/claude-code).

## Plugins

| Plugin | Description |
|--------|-------------|
| [todo-list](plugins/todo-list/) | GTD-powered task management skills for Todoist |

## Installing Plugins

```bash
claude plugin install <plugin-url>
```

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for how to submit a plugin.

## Structure

Each plugin lives in its own directory under `plugins/`:

```
plugins/
└── my-plugin/
    ├── .claude-plugin/
    │   └── plugin.json      # Plugin manifest
    ├── commands/             # Slash commands
    ├── agents/               # Subagent definitions
    ├── skills/               # Agent skills
    ├── hooks/                # Event hooks
    └── README.md
```
