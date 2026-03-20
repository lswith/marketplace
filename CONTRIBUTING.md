# Contributing a Plugin

## Adding a New Plugin

1. Create a directory under `plugins/` with your plugin name (kebab-case)
2. Add a `.claude-plugin/plugin.json` manifest
3. Add your components (commands, agents, skills, hooks, etc.)
4. Include a `README.md` describing what the plugin does
5. Submit a pull request

## Plugin Requirements

- Must have a valid `plugin.json` with at least `name`, `version`, and `description`
- Must include a `README.md`
- Should follow semantic versioning
- Must not include secrets or credentials
