# learn

A Claude skill to learn any subject in depth, across many conversations, without losing what you understood.

## The problem

Learning with Claude works well inside a conversation. Then the conversation ends, and what you understood is gone:
- insights scattered across dozens of chats,
- reference docs lost or rebuilt from fragments,
- every new session starting from zero.

## The rule

**The conversation is a trace. The reference lives elsewhere.**

This skill keeps the reference in [Relinkia](https://relinkia.com), connected to Claude over MCP. Every note is versioned, protected against conflicting writes, and readable from any session: claude.ai on the web or on your phone, and Claude Code.

## How it works

1. **Start from an anchor**: a real question, a post, a paper, a chapter.
2. **Descend one concept at a time.** Each concept is called for by a question raised by the previous one. Explanations follow a fixed format: answer first, worked numeric example, "why here and not elsewhere", misconceptions, code.
3. **Say "capture".** Claude writes:
   - **one note per concept**: problem solved, intuition, mechanism, why here, comparison, misconceptions, practice, 3 recall questions, links;
   - **one map**: what you know, and the **frontier** of what you've spotted but not studied yet.
4. **Next session**, Claude rereads the map and picks up from what you know.

## Example

A real descent, starting from a post about JEPA world models:

latent space → SIGReg → BatchNorm → LayerNorm → RMSNorm → attention

<!-- TODO: add screenshots of the map (with its frontier) and of one concept note -->

## Install

**Claude Code**: copy the `learn/` folder into `.claude/skills/` (in your project or your home directory).

**claude.ai**: add the skill from your settings.

**Relinkia**: <!-- TODO: how to get access and connect the Relinkia MCP server -->

## Without Relinkia

The skill has a fallback mode for Claude Code: a folder of markdown files (`map.md` plus one file per concept), same templates and rituals. You lose versioning, conflict protection and access from claude.ai and your phone, but you keep the method.

