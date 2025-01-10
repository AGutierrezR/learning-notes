# TMUX + GIT WORKTREE

```bash
tmux new-session -ds rewards-promotions-futura -c $(git wtl | fzf | awk '{print $1}')
```
