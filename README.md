# tinkerbench-studio plugins

One Claude Code marketplace for every tinkerbench-studio plugin. Each plugin lives and is released in
its own repository; this repository only lists them, so a project adds one marketplace and names
each plugin as `<plugin>@tinkerbench-studio`.

| Plugin | Repository | What it is |
| --- | --- | --- |
| `tick-it` | [tinkerbench-studio/tick-it-claude-mod](https://github.com/tinkerbench-studio/tick-it-claude-mod) | Tick-it tickets, board and review agents in the session |
| `drawing-board` | [tinkerbench-studio/drawing-board](https://github.com/tinkerbench-studio/drawing-board) (`plugin/`) | Design workflows: prototype first, canvas and Storybook in step, flow pages, UX pictures |
| `vibesec` | this repository (`plugins/vibesec/`) | `VibeSec-Skill`: secure-web-application guidance, for any project that writes or audits web code |

## Using it in a project

In the project's `.claude/settings.json`:

```json
{
  "extraKnownMarketplaces": {
    "tinkerbench-studio": { "source": { "source": "github", "repo": "tinkerbench-studio/marketplace" } }
  },
  "enabledPlugins": {
    "tick-it@tinkerbench-studio": true,
    "drawing-board@tinkerbench-studio": true,
    "vibesec@tinkerbench-studio": true
  }
}
```

In a cloud environment's setup script:

```bash
claude plugin marketplace add tinkerbench-studio/marketplace
claude plugin install tick-it@tinkerbench-studio
claude plugin install drawing-board@tinkerbench-studio
claude plugin install vibesec@tinkerbench-studio
```

A project that adds `vibesec` deletes its own `.claude/skills/VibeSec-Skill`: the plugin's skill is that
same text, and a local copy would be a second one to keep in step.

All the repositories are private. Claude Code clones them with the git credentials the machine
already has (an SSH key, or an HTTPS credential such as `gh auth setup-git`), so the environment's
GitHub access must cover this repository and every plugin repository it lists.

## Adding a plugin

A plugin whose source is small and used only through this marketplace can live here, in `plugins/<name>/`
(`vibesec` does), with a relative `source` such as `"./plugins/vibesec"`. Otherwise add an entry to
`.claude-plugin/marketplace.json` with a `git-subdir` source (its repository and the
folder holding `.claude-plugin/plugin.json`), then run `claude plugin validate .`.
