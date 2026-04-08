# Rebase — reference

## Conflict marker reminder

During `git rebase`, **ours** = the commits you are replaying (the branch being rebased); **theirs** = the commit you are rebasing onto (upstream). This is the opposite of a normal merge in some mental models — when confused, trust `git status` and `git diff` names for the current step.

## Useful commands

| Goal                      | Command                                                                                  |
| ------------------------- | ---------------------------------------------------------------------------------------- |
| See conflicts             | `git status`                                                                             |
| Diff conflict stages      | `git diff` / `git diff --cc <file>`                                                      |
| History touching a file   | `git log --oneline --follow -- <path>`                                                   |
| Who changed a line        | `git blame -L <start>,<end> <path>`                                                      |
| List conflicted files     | `git diff --name-only --diff-filter=U`                                                   |
| Skip a commit (dangerous) | Only if user explicitly wants `git rebase --skip` — verify the commit is empty/redundant |

## Integrating overlapping refactors

If upstream renamed or moved code while the branch edited the old location:

1. Find the new location on the base (`git log --follow`, search symbols).
2. Re-apply the branch’s logical change against the new structure instead of pasting the old hunk.
3. Delete dead code left from the old path if upstream removed it intentionally.

## After rebase completes

- If the branch was already pushed: the user needs `git push --force-with-lease` (or a new branch). Ask if they want to push the changes. If they confirm they do, force push the checked out branch to the remote.
- Run relevant tests or linters if available and proportionate to the conflict scope.
