<p align="center">
  <img src="https://folkso.app/brand/folkso-app-icon.png" width="112" height="112" alt="Folkso">
</p>

<h1 align="center">Folkso</h1>

<p align="center">
  The talent agent for your AI. Works in ChatGPT, Claude, Claude Code and Codex.<br>
  <a href="https://folkso.app">folkso.app</a> · <a href="https://folkso.app/help">Help</a> · <a href="https://folkso.app/privacy">Privacy</a>
</p>

<br>

Tell your AI who you need and how you like to work together. Folkso shows real people who filled in a profile and chose to appear in AI answers. People come to it for jobs and paid projects, startup teams, mentoring and meeting up in their city.

<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://folkso.app/brand/folkso-demo-dark.gif">
    <img src="https://folkso.app/brand/folkso-demo-light.gif" width="600" alt="Folkso in ChatGPT and in Claude: someone asks for a photographer, a sales manager, a co-founder and people to play board games with, and Folkso shows matching people as cards">
  </picture>
</p>

## Install

**ChatGPT.** Install Folkso from the ChatGPT plugin directory and sign in. [Step by step](https://folkso.app/help#chatgpt)

**Claude.** Add Folkso in Settings, Connectors, and sign in. It then works in the Claude apps and in Claude Code on the same account. [Step by step](https://folkso.app/help#claude)

**Claude Code**

```bash
claude plugin marketplace add saplq/folkso-plugin
claude plugin install folkso@folkso
```

**Codex**

```bash
codex plugin marketplace add saplq/folkso-plugin
codex plugin add folkso@folkso
codex mcp login folkso
```

You sign in with Google or an email code. In Claude Code and Codex you can also paste the [setup prompt](https://folkso.app/help#agents), and the agent installs Folkso itself.

## Try it

```text
Find a React developer in Europe for a contract up to $6,000 a month
Who in Lisbon can shoot a family photo session on Saturday?
Did Maria reply to my request?
Help me create my Folkso profile
```

Your AI shows people as cards. Open one with **Details**, and ask it to write to the person. A request goes out only after you see the preview and confirm it.

## What's inside

| Path                              | What it does                                               |
| --------------------------------- | ---------------------------------------------------------- |
| `skills/folkso`                   | Tells the AI when to call Folkso and when to ask you first |
| `.mcp.json`                       | Connects the Folkso server, `https://folkso.app/api/mcp`   |
| `.claude-plugin`, `.codex-plugin` | The plugin for Claude, and for ChatGPT and Codex           |
| `.agents/plugins`                 | Lets Codex install the plugin from this repository         |

## Privacy

- Folkso gets the conditions of your task and a short summary of it. It never reads your chat history or your AI's memory.
- Other people's contacts never reach the model. You swap contacts in Folkso after the person accepts your request.
- Your own contacts reach the model masked.

Questions go to [hello@folkso.app](mailto:hello@folkso.app). [Privacy policy](https://folkso.app/privacy) · [Terms](https://folkso.app/terms)

## License

MIT
