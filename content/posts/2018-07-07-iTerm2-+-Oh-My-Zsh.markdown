---
layout: post
title:  "iTerm2 + Oh My Zsh"
date:   2018-07-07
categories: ['web development']
tags: ['tool']
---

### Install iTerm2

```bash
$ brew cask install iterm2
```

Or install iTerm2 from https://www.iterm2.com/

### Install Oh My Zsh

Via cul:

```bash
$ sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

Via wget:

```bash
$ sh -c "$(wget https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
```

### Install Powerline

```bash
$ pip install powerline-status --user
```

You may need to install pip first:

```bash
$ sudo easy_install pip
```

### Install a patched font

https://github.com/powerline/fonts

https://github.com/Falkor/dotfiles/blob/master/fonts/SourceCodePro%2BPowerline%2BAwesome%2BRegular.ttf

### Install a theme

https://github.com/Powerlevel9k/powerlevel9k

### Enable word jumps and word deletion, aka natural text selection

By default, word jumps (option + → or ←) and word deletions (option + backspace) do not work. To enable these, go to "iTerm → Preferences → Profiles → Keys → Load Preset... → Natural Text Editing"

### Custom prompt styles

By default, your prompt will now show “user@hostname” in the prompt. This will make your prompt rather bloated. To remove this you can add the line DEFAULT_USER=$(whoami)to ~/.zshrc.
