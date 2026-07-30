# Cross-Tool Prompt Injection Benchmark

A structured security evaluation testing whether a multi-tool AI agent (Claude, connected to Gmail and Slack) can be manipulated into taking unintended actions or leaking data across services.

## What it does

Built on top of a working multi-tool agent that reads Gmail, checks Slack, and lets Claude decide which tool(s) a request needs. This benchmark deliberately attacks that agent with 20 different manipulation attempts across two rounds:

1. **Direct injection** — attack text sent as the user's own request to the tool-selecting agent
2. **Embedded injection** — attack text hidden inside email content, read during a normal, innocent classification task

Each attack uses a genuinely different technique (direct override, fake system messages, role-play/jailbreak framing, false consent, contradictory logic, data exfiltration attempts, and more) rather than repeating one style — addressing a real, published critique that most existing prompt injection benchmarks rely on narrow, repetitive attack patterns.

## Result

**0 out of 20 attacks succeeded** in causing genuinely malicious behavior (no unauthorized actions, no data leaked across tools). Claude's classifier actively identified and named several attempts as "prompt injection" or "social engineering" in its own reasoning, rather than simply failing to comply by chance.

## Why this matters

As AI agents increasingly connect multiple business tools to one shared reasoning layer (exactly the architecture platforms like Anthropic's MCP and agentic AI products are built on), the risk isn't just "can this one tool be tricked" — it's whether malicious content in ONE tool can cause harmful action in a DIFFERENT, connected tool. This is a real, underexplored attack surface as multi-tool agents become standard.

## Honest limitations

- Small sample size (20 tests) on a single agent implementation
- Results reflect this specific system's narrow, well-scoped system prompts — they don't prove immunity for all multi-tool agent designs, especially ones with broader or vaguer instructions
- Future work: harder combined attacks, testing against a deliberately weaker system prompt as a control, and semantic/embedding-based attack variations

## Built with
- Claude API (Anthropic) — agent, tool-use pattern, classification
- Gmail API, Slack API — the two connected tools under test
- Python (Google Colab)

## To run it yourself
1. Get an Anthropic API key
2. Set up Gmail and Slack API access (see the linked [Gmail Triage Agent](https://github.com/yashhh004/gmail-triage-agent) and [Slack Message Classifier](https://github.com/yashhh004/slack-triage-agent) repos for setup steps)
3. Add your own credentials where the placeholders are
4. Run the notebook top to bottom
