# tinkerbench-studio plugins

One Claude Code marketplace for every tinkerbench-studio plugin. Each plugin lives and is released in
its own repository; this repository only lists them, so a project adds one marketplace and names
each plugin as `<plugin>@tinkerbench-studio`.

| Plugin | Repository | What it is |
| --- | --- | --- |
| `tick-it` | [tinkerbench-studio/tick-it](https://github.com/tinkerbench-studio/tick-it) (`mod/`) | Tick-it tickets, board and review agents in the session |
| `drawing-board` | [tinkerbench-studio/drawing-board](https://github.com/tinkerbench-studio/drawing-board) (`plugin/`) | Design workflows: prototype first, canvas and Storybook in step, flow pages, UX pictures |

## Using it in a project

In the project's `.claude/settings.json`:

```json
{
  "extraKnownMarketplaces": {
    "tinkerbench-studio": { "source": { "source": "github", "repo": "tinkerbench-studio/marketplace" } }
  },
  "enabledPlugins": {
    "tick-it@tinkerbench-studio": true,
    "drawing-board@tinkerbench-studio": true
  }
}
```

In a cloud environment's setup script:

```bash
claude plugin marketplace add tinkerbench-studio/marketplace
claude plugin install tick-it@tinkerbench-studio
claude plugin install drawing-board@tinkerbench-studio
```

All three repositories are private. Claude Code clones them with the git credentials the machine
already has (an SSH key, or an HTTPS credential such as `gh auth setup-git`), so the environment's
GitHub access must cover this repository and every plugin repository it lists.

## Adding a plugin

Add an entry to `.claude-plugin/marketplace.json` with a `git-subdir` source (its repository and the
folder holding `.claude-plugin/plugin.json`), then run `claude plugin validate .`.
