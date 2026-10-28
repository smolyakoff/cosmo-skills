---
name: manage-worktrees-like-cosmo
description: Where git worktrees go. Use before creating or moving one, including for a branch review or a hand-off to another session or sub-agent.
---

# Manage Worktrees

Keep worktrees in plain sight, in a well-structured directory tree inside the workspace where the user works. Tool-specific
folders such as `.claude/worktrees/` hide them from the user.

## Concepts

**Workspace**: a folder containing all the git checkouts.

**Container Repo**: a plain folder containing worktrees related to a single repo.

**Slot**: a long-lived worktree with a fixed purpose. Reuse it: switch the existing slot to the branch you need instead
of adding another worktree.

**Author**: the commit author of the branch under review, written as the first letter of the first name plus the last
name, lowercased, like `jsmith`. The user's own branches get a review slot the same way.

## Folder Layout

Every checkout lives at `<workspace>/<repo>/<repo>-<purpose>/`. `<repo>` is the remote repo's name, and the container
repo is a plain folder, not a git repo itself. `small`, `support` and `review-<author>` are slots.

| `<purpose>` | Use |
|---|---|
| `main` | The clone with the git directory. Main work, on any branch. |
| `small` | Small changes on the side of the main work. |
| `support` | Troubleshooting, like reproducing a bug. |
| `review-<author>` | Reviews of one author's branches, not one per pull request. |
| `temp-<name>` | One throwaway task, named after it. Remove it when the task is done. |

For example:

```text
workspace/
└── shop/
    ├── shop-main/
    ├── shop-review-jsmith/
    └── shop-temp-upgrade-node/
```

## Reorganizing

When asked to reorganize, or when you meet a clone outside a container repo, propose the moves into this layout, with
the clone becoming `<repo>-main`. Wait for the user's yes before moving anything.
