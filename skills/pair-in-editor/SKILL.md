---
name: pair-in-editor
description: Pair live in your editor. The human writes feedback in a markdown file and TODOs in the code, and the agent applies each thought as soon as the human finishes it.
disable-model-invocation: true
---

# Pair in Editor

You pair with the human on a change. They read your work in their editor and give feedback in two places:

- **The feedback file**: `.ai-feedback.md` in the repo root, unless the human names another file. High-level notes as
  list items, lines separated by blank lines, or sections under headers. The file is optional.
- **TODOs in code**: `TODO` comments that appear during the session. At the start, record the TODOs already in the
  working tree in your log. Any other TODO is feedback, wherever it lands and whatever the human commits.

Apply each thought as soon as the human finishes it, while they keep writing the next one.

The human works in the same files. They may commit whole files or chunks, and make small edits of their own. Their own
edits are not feedback: keep them as they are.

Their editor may hold unsaved changes that overwrite yours on the next save. Edit a file only after it has been quiet
for a short while, and re-read it right before you write. Redo your edit if their next save drops it.

## When a thought is complete

In the feedback file, an item is complete once a separator follows it:

- a blank line,
- a new list item (`-`, `*`, `1.`),
- a header,
- a line with `END`.

A single newline is not a separator: a thought can span several lines, and editors may add a final newline on save.
Wait for a separator after the last item.

In code, a TODO is complete on the first of these signals:

- It ends with `END`.
- The human moved on: they edited another place in the code or the feedback file after it.
- The file has been quiet for a short while.

## Loop

1. Read the feedback file, the new TODOs, and your log. Find complete thoughts you have not
   applied yet.
2. Apply each thought. Delete a code TODO as part of its fix. Leave the feedback file as it is: it belongs to the human.
3. When a thought is unclear, or you want to ask before you change the code, reply next to the most related code with an
   `AI REPLY:` comment in the file's comment syntax. The human answers in the feedback file or with a comment near
   yours. Delete your reply once you act on the answer.
4. Record the thought in your log and post one line in chat: the thought and what you did.
5. Wait for the next change in the working tree that is not your own, and go back to step 1.

## Progress log

Keep the log outside the repo, in the OS temp directory. Derive its name from the repo path, so you find it again after
your context is compacted. For example: `<temp>/pair-in-editor/<repo path with / replaced by ->.log`.

Record each applied thought by its text. The human closes a feedback item by deleting it. Drop it from the log then.

## Stopping

Stop when the feedback file has a `STOP` line or the human asks in chat to end pairing. First apply the complete
thoughts above `STOP`. Then summarize what you applied and what is still open: unanswered replies and incomplete items.

## Version control

Leave every commit to the human. Never commit or stage anything during the session, and never add the feedback
file to version control.
