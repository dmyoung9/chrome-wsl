# chrome-wsl

This is a simple Augment plugin that includes the following:

- "Slim" configuration of the [Chrome DevTools MCP](https://github.com/ChromeDevTools/chrome-devtools-mcp)
- WSL compatibility [`chrome-wsl`](https://github.com/dbalabka/chrome-wsl) wrapper hook
- `@browser` subagent
- Commands for quick testing

## Installation

### Requirements

- [Auggie CLI](https://docs.augmentcode.com/cli/overview) >= `0.23.0` ([plugin support introduced](https://www.augmentcode.com/changelog/cli-0-23-0-release-notes))
- [Windows Subsystem for Linux (WSL)](https://learn.microsoft.com/en-us/windows/wsl/install) (not much point being here without this :stuck_out_tongue_winking_eye:)

### Instructions

```sh
# Add the marketplace
> auggie plugin marketplace add dmyoung9/chrome-wsl

# Install the plugin
> auggie plugin install chrome-wsl@chrome-wsl
```

## Usage

With the plugin installed and enabled, `auggie` can access the Chrome DevTools MCP. When running `auggie` in WSL, a `PreToolUse` hook will be run before any `chrome-devtools` tool call, to ensure that an instance of Chrome is _running in the Windows host_ for the MCP to use. A `SessionEnd` hook closes the Chrome instance when the session ends.

### Commands

This plugin comes with two demonstrative commands:

| Command                   | Description                                                                         |
| ------------------------- | ----------------------------------------------------------------------------------- |
| `/browser:main <url>`     | Instruct the main agent to navigate to `url`                                        |
| `/browser:subagent <url>` | Instruct the main agent to delegate to the `@browser` subagent to navigate to `url` |

---

> [!NOTE]
> As of `auggie==0.26.0`, subagent sessions do not fire hook events, so the `PreToolUse` hook **_will not_** be able to start a Chrome session inside Windows automatically.
>
> Alternative options include using the standard WSL-supervised Chrome instance (see [here](https://github.com/ChromeDevTools/chrome-devtools-mcp#getting-started)) or starting the Windows-supervised instance manually, using [`@dbalabka/chrome-wsl`](https://github.com/dbalabka/chrome-wsl).
