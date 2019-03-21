---
description: >-
  I really like using the command line and I always try to learn something new
  from time to time. Here are a few programs I like the most.
---

# Terminal

## oh my zsh

[Oh my zsh](https://ohmyz.sh/) is a framework to to managing your [zsh](http://www.zsh.org/) configuration.

Long story short, you have a single configuration file and a better terminal experience.

For example you can change your terminal to always show the branch name so you don’t need to run `git branch` to know that. You can also add many other things like show a  if you have changes in your code, how many items you have on your `stash`, etc.

I’ve seen people using it in a bunch different ways, but I stick the basics like using a few plugins and not too much customizations.

You can check my configuration file [here](https://github.com/lucasprag/dotfiles/blob/master/zshrc).

## xargs

`xargs` builds and executes command lines given an input. It’s specially useful after `grep`ing. For example:

```text
git branch | grep bugfix | xargs git branch -D
```

`xargs` is going to execute `git branch -D` for each branch name listed from `git branch | grep bugfix`

## awk

AWK is a programming language designed for text processing. It has a bunch of features which I should take some time to learn, but I mainly use it for getting the content of a column given a command result.

For example if you run `ps aux` in the command line, you’d get a result like this:

```text
youruser     2073   0.0  0.1  2462832   5012 s001  Ss   10:08PM   0:00.99 program1
youruser     1954   0.0  0.0  2463092   3576   ??  Ss   10:08PM   0:04.17 program2
youruser     1952   0.0  0.0  2445684   1352 s000  S+   10:08PM   0:00.01 program3
```

If you want to get the process id \(aka `pid`\) to `kill` it you only need the content of the second column.

With `awk` you can do it like this:

```text
ps aux | grep program1 | awk '{print $2}' | xargs kill
```

## ssh

### **easy access to your servers**

You can save some configs to easy access your servers into `~/.ssh/config` and they look this:

```text
Host my_server
  User ubuntu
  IdentityFile /path/to/your/key.pem
  HostName ec2-123-123-123-123.compute-1.amazonaws.com
```

so you can access your server with `ssh my_server`.  


### **copy files over ssh**

* to copy from your machine to the server: `scp myfile.txt my_server:/home/ubuntu/myfile.txt`
* to copy from your server to your machine: `scp my_server:/home/ubuntu/myfile.txt myfile.txt`

## **A**lacritty

[Alacritty](https://github.com/jwilm/alacritty) is a cross-platform, GPU-accelerated terminal emulator that I use in a day-to-day basis. It’s pretty fast over [iTerm](https://www.iterm2.com/).

It requires a configuration file if you need to change things like font family or font size, because there is no interface to change it which I don’t think it’s a problem for programmers.

It doesn’t have features like tabs and splits so for that you need [tmux](tmux.md).

[This](https://github.com/lucasprag/dotfiles/blob/master/alacritty.yml) is my config for Alacritty.

