# Skills

This repo is my current agent skills. Claude Code and pi have symlinks to the `~/.agents/skills` directly.

The main sources for my skills are from: 

- [mattpocock/skills](https://github.com/mattpocock/skills)
- [cursor/plugins, pstack](https://github.com/cursor/plugins/tree/main/pstack)

## How I use skills

Most of these are user-invoked: they run when I type `/name`, and the agent doesn't know about them. 

I want to see what each model can do by itself as new ones come out, without my skills shaping every answer. That's also why I keep Claude's memory turned off. 

The few that are model-invoked are ones I'd want on every time the situation comes up, like writing without AI slop (using the `unslop` skill from pstack).

