# Relinkia skills

Claude skills that work from a canonical memory stored in [Relinkia](https://relinkia.com), instead of from chat history.

**The rule behind all of them: the conversation is a trace, Relinkia is the reference.** Notes are versioned, protected against conflicting writes, and readable from any session: claude.ai on the web or on your phone, and Claude Code.

## Skills

| Skill | What it does |
|---|---|
| [`learn`](learn/) | Learn any subject in depth across conversations: one note per concept, and a map of what you know and what you don't know yet. |

## Install

**Claude Code**: copy a skill folder (e.g. `learn/`) into `.claude/skills/`, in your project or your home directory.

**claude.ai**: add the skill from your settings.

Relinkia: create a free account at https://relinkia.com, then connect its MCP server to Claude (see the docs).

Each skill's own README says whether it has a fallback mode without Relinkia.

## License

MIT
