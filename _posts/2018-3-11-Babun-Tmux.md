# Configuring Babun & Tmux

1. Configure Babun to copy paste with keyboard

  `Ctrl + c` or `Ctrl + v` does not natively work, this is because of terminal shells generally use `Ctrl + c` in order to cancel execution babun. In Babun the shortcut is `Shift + insert`

2. Configure copy paste with mouse

  After reading this [post](https://stackoverflow.com/questions/17445100/getting-back-old-copy-paste-behaviour-in-tmux-with-mouse I found that I need  to hold shift toggle during mouse text selection (copy) I realized Babun expects you to hold `Shift` while you select (copying) and while your righ-click (pasting).

3. Update alias for common commands

  I had forgotten that the default behaviour of the ls command did not include color so i added the following alias to .zshrc

      ```bash
      ## Colorize the ls output ##
      alias ls='ls --color=auto'

      ## Use a long listing format ##
      alias ll='ls -la'

      ## Show hidden files ##
      alias l.='ls -d .* --color=auto'
      ```

4. Configure zshell theme

  Initially I was installing and playing around with themes and i reverted back to one of the default  installed themes that came with babun because other themes where extremely slow. Issue was reported [here](https://github.com/babun/babun/issues/48) as well.

  I then proceeded to follow this [guide](https://www.dasblattwerk.at/webdev-workbench-01-shell/) and now have a great working environment.

  **NOTE:**  Had to install the Powerline themes to windows: `C:\Windows\Fonts`

5. Configure Tmux

  Added the following changes:  
  * mouse support
  * better mapping for window splitting
  * ability to navigate panes using arrow keys  

  To do this, modify `.tmux.conf` to include the following:

  ```bash
  # Appeareance
  set -g default-terminal "screen-256color"
  source-file "${HOME}/.tmux-themepack/powerline/block/green.tmuxtheme"

  # Windows Handling
  bind | split-window -h
  bind - split-window -v

  # Send-prefix to nested ssh'ed tmux session
  bind-key -n C-g send-prefix

  # Shift arrow to switch panes
  bind -n S-Left  select-pane -L
  bind -n S-Right select-pane -R
  bind -n S-Up    select-pane -U
  bind -n S-Down  select-pane -D

  # reload config file (change file location to your the tmux.conf you want to use)
  bind r source-file ~/.tmux.conf

  # Enable mouse control (clickable windows, panes, resizable panes)
  set -g mouse on
  ```
  The theme was downloaded by following these [instructions](https://github.com/jimeh/tmux-themepack):

  ```bash
  git clone https://github.com/jimeh/tmux-themepack.git ~/.tmux-themepack
  ```
