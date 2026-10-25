---
name: rethink-comments
description: Rethink the comments and developer-facing messages in the current change. Drops every comment, re-adds only the good ones, and marks each message for human review. Use before opening a PR, or when asked to rethink comments or messages.
---

# Rethink Comments

Polish the wording of a change before other developers read it. You rethink the comments and developer-facing messages.
The human reviews your edits and every message.

## Scope

The change is the diff between the current branch and its merge base with the default branch. If there is no merge
base, ask the human what the change is. Rethink the comments and developer-facing messages
it adds or modifies. Developer-facing messages are error and exception messages, log lines, CLI output, and assertion
messages. UI text is out of scope. Docstrings and other documentation comments count as comments.

## Preconditions

Stop and tell the human when either fails:

- Every file you are about to edit has no uncommitted changes. This keeps your edits in a diff of their own. If the
  change itself is not committed yet, ask the human to commit it first.
- No `TODO(rethink-comments):` marker is left in the change. A marker means the human has not finished reviewing an
  earlier pass. List the files that hold markers.

## Steps

1. Drop every comment in scope, except these, which you keep exactly as they are:
   - Comments that tools read, such as lint directives, license headers, and pragmas.
   - Work items such as `TODO` and `FIXME`.
2. Re-add only [good comments](#good-comments). Write each one fresh, from what you know about the change: why the code
   looks the way it does, and what the code cannot show.
3. Rewrite each developer-facing message in scope when you can make it clearer. A good message tells the developer what
   went wrong and what to do next.
4. Put `TODO(rethink-comments): review the message below` on the line above every message in scope, in the file's
   comment syntax. Mark the messages you left unchanged too: the marker means a human has not looked yet.

You are done when every comment and message in scope is handled. Report the files that hold markers. The human
reviews your diff and deletes each marker once the message is right.

## Good comments

A comment that repeats its code or its name is noise. A good comment says what the code cannot.
Judge "obvious" as a developer who reads the code for the first time, not as its author.

- **Why**: the reason for a non-obvious choice or a workaround. A reason future developers need belongs in the code, not
  only in the commit message.
- **Precise details** a name cannot carry. When a better name would carry the meaning, rename instead.
- **Purpose**: what a function, class, or field is for, when its name and signature cannot say it all. For a long
  function, what each block does.
- **Effects elsewhere**: a warning about a surprising edge case or a side effect in another part of the system.

Classic books say it better:

- _A Philosophy of Software Design_ by John Ousterhout
- _Clean Code_ by Robert C. Martin
