# clay-debate-setup

Design structured debates between your AI teammates. A debate setup skill for [Clay](https://github.com/chadbyte/clay)'s Mates system.

When you start a debate in Clay, this skill helps the moderator Mate prepare: refining the topic, choosing a format, and assigning roles to panelists based on their personalities.

## Prerequisites

- [Clay](https://github.com/chadbyte/clay) must be installed and running. Debates is a Clay feature. This skill is used by Clay to prepare the debate before the debate engine takes over.

## Install

```bash
npx skills add chadbyte/clay-debate-setup
```

## What it does

When a debate is initiated from a Mate's DM, the skill:

1. **Reads the team** by checking each panelist's CLAUDE.md, bio, and past session digests
2. **Refines the topic** through conversation (a vague "AI ethics" becomes "Should the EU AI Act be applied globally?")
3. **Chooses a format** based on topic and panelist count (pro/con, round table, devil's advocate, etc.)
4. **Assigns roles** that match (or deliberately contrast) each Mate's personality and expertise
5. **Outputs a debate brief** that Clay's debate engine consumes to run the actual debate

## How it works

```
+--------------+     +--------------+     +--------------+     +--------------+
|   Debate     |---->|    Setup     |---->| Debate Brief |---->| Debate Loop  |
|   Modal      |     | (this skill) |     |  generated   |     |   (engine)   |
| (topic+panel)|     |              |     |              |     |              |
+--------------+     +--------------+     +--------------+     +--------------+

Modal: user picks initial topic + panelists
Setup: moderator Mate refines topic, assigns roles via conversation
Brief: structured JSON with topic, format, roles, context
Engine: moderator runs the debate via @mentions (not this skill)
```

- The moderator Mate speaks as itself, not as a generic facilitator
- Adapts pace to the user. Eager users get 2 questions. Thorough users get a full design session
- Role suggestions are grounded in actual Mate personalities, not generic assignments
- The skill ends at the brief. The debate engine handles the actual debate

## Usage

Triggered when starting a debate from a Mate's DM in Clay's UI. Can also be invoked manually:

```
/clay-debate-setup
```

## License

MIT
