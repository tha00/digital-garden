---
title: Tmux shortcuts
draft: false
tags:
---
 
[Tmux Cheat Sheet](https://tmuxcheatsheet.com/)

Leader key: `^a`  (default is `^b`)

Command mode: leader + `:`

Meta:
* Start new session : `tmux`
* Detach: leader + `d`
* Attach: `tmux attach`
* List sessions: leader + `s`
* Kill session: command mode + `kill-session`

Panes:
* Split pane vertically: leader + `%`
* Split pane horizontally: leader + `"`
* Close pane: leader + `x`

Windows:
* New window: leader + `c`
* Break pane (i.e. move current pane to a new window): leader + `!`
* Select window by number: leader + `0..9`
* Go to previous window: leader + `p`
* Go to next window: leader + `n`
