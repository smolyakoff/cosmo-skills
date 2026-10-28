# Unpopular agent skills

They won't make you a 10x engineer, but I find them useful now and then. Why `cosmo-skills`? I couldn't come up with a
better name. Besides, **Co**nstantine **Smo**lyakov is just another way to spell my name 😊.

> [!NOTE]
> These skills are experimental, and I'm still polishing them, so expect changes.

## How to install

Use [Vercel's skills CLI](https://github.com/vercel-labs/skills):

```bash
# Install all skills
npx skills add smolyakoff/cosmo-skills

# Cherry-pick skills
npx skills add smolyakoff/cosmo-skills --skill pair-in-editor-like-cosmo
```

## Why use them

### Pair in editor

For when you still want to read the code, maybe because you like it.

- **Agent:** writes the code and listens for the human's feedback live.
- **Human:** writes big-picture notes in `.ai-feedback.md` and leaves TODOs in the code.

You work in parallel, as in [pair programming](https://en.wikipedia.org/wiki/Pair_programming). The code changes as
soon as you finish a thought. It can get messy, so embrace the fun!

### Rethink comments

Agents are known to write lots of comments, and they don't always write well for humans.

As a human, I do the bulk of the work first and polish at the end. The polish includes:

- Thinking through the caveats and hard parts, and keeping comments only where they are really needed.
- Making developer-facing messages clear: error messages, log lines, CLI output. The developer who hits one should know
  what went wrong and what to do next.

This skill turns that habit into a step before you share the change:

- **Agent:** drops every comment in the changed code, then re-adds only the useful ones. Marks every developer-facing
  message for review.
- **Human:** reviews the agent's diff, so the change goes out with comments and messages that help the next
  developer.
