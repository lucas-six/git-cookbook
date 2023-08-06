# Bash Prompt String for Git

## Usage

```bash
# bash_profile

# Git: bash prompt string for branches
export PS1="\u@\h:\w\[\033[32m\]\$(git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/')\[\033[00m\]$ "
```
