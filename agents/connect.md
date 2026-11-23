# Connect an AI agent

> Every agent Skryvo has setup steps for, how each one signs in, and the guide that walks through it.

Every agent connects to the same server, `https://api.skryvo.ai/mcp`. Agents that support OAuth sign the person in through Skryvo's consent page; the others send an API key made in **Settings › API & agents**. The same list, with each agent's steps and an Open button where the agent has one, is in Skryvo under Settings › API & agents.

Each agent's step-by-step guide stays at its own page under [/agents/](https://skryvo.ai/agents/); the table links to it.

| Agent | Signs in with | Guide |
|---|---|---|
| Claude | OAuth sign-in | [Set up Claude](https://skryvo.ai/agents/claude/) |
| Claude Cowork | OAuth sign-in | [Set up Claude Cowork](https://skryvo.ai/agents/claude-cowork/) |
| Claude Code | OAuth sign-in | [Set up Claude Code](https://skryvo.ai/agents/claude-code/) |
| ChatGPT | OAuth sign-in | [Set up ChatGPT](https://skryvo.ai/agents/chatgpt/) |
| OpenAI dots | OAuth sign-in | [Set up OpenAI dots](https://skryvo.ai/agents/openai-dots/) |
| Codex | OAuth sign-in | [Set up Codex](https://skryvo.ai/agents/codex/) |
| Cursor | OAuth sign-in | [Set up Cursor](https://skryvo.ai/agents/cursor/) |
| VS Code | OAuth sign-in | [Set up VS Code](https://skryvo.ai/agents/vscode/) |
| Gemini | OAuth sign-in | [Set up Gemini](https://skryvo.ai/agents/gemini/) |
| Grok Build | OAuth sign-in | [Set up Grok Build](https://skryvo.ai/agents/) |
| Grok Bot | API key | [Set up Grok Bot](https://skryvo.ai/agents/grok-bot/) |
| Perplexity Computer | OAuth sign-in | [Set up Perplexity Computer](https://skryvo.ai/agents/perplexity/) |
| Kimi Code | OAuth sign-in | [Set up Kimi Code](https://skryvo.ai/agents/kimi-code/) |
| Muse | OAuth sign-in | [Set up Muse](https://skryvo.ai/agents/muse/) |
| Windsurf | OAuth sign-in | [Set up Windsurf](https://skryvo.ai/agents/windsurf/) |
| Manus | OAuth sign-in | [Set up Manus](https://skryvo.ai/agents/manus/) |
| Cue | API key | [Set up Cue](https://skryvo.ai/agents/) |
| DeepSeek | API key | [Set up DeepSeek](https://skryvo.ai/agents/deepseek/) |
| OpenClaw | API key | [Set up OpenClaw](https://skryvo.ai/agents/openclaw/) |
| Hermes Agent | API key | [Set up Hermes Agent](https://skryvo.ai/agents/hermes/) |
| NanoClaw | API key | [Set up NanoClaw](https://skryvo.ai/agents/) |
| Paperclip | API key | [Set up Paperclip](https://skryvo.ai/agents/) |
| Any MCP client | OAuth sign-in | [Set up Any MCP client](https://skryvo.ai/agents/) |
| Scripts & n8n | API key | [Set up Scripts & n8n](https://skryvo.ai/agents/api/) |

## Any other MCP client

Add the address as a remote MCP server over Streamable HTTP. A client with OAuth signs the person in; any other sends the key as a header:

```text
https://api.skryvo.ai/mcp
Authorization: Bearer YOUR_SKRYVO_API_KEY
```

## Check it works

Ask the agent "List my Skryvo brands". It should call `list_brands` and name the person's brands. "Which channels can post for my brand?" calls `list_channels`.

## Plugins and skills

The plugins for Claude Code, Cursor and Grok, the Gemini extension, a generic MCP setup and two skills are in the public repository [github.com/Skryvo/agent](https://github.com/Skryvo/agent), under the MIT licence. The `skryvo-api` skill calls the REST API with `SKRYVO_API_KEY`, for agents that take skills but no MCP server.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/agents/connect/
