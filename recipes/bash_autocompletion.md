# Bash Autocompletion for Git

## Recipes

### Installation

```bash
curl https://raw.githubusercontent.com/git/git/master/contrib/completion/git-completion.bash -o ~/.git-completion.bash
# curl https://gitee.com/liwg06/git/raw/master/contrib/completion/git-completion.bash -o ~/.git-completion.bash

chmod +x ~/.git-completion.bash
```

### Usage

```bash
# bash_profile

# Git: bash auto-completion
if [ -f ~/.git-completion.bash ]; then
    source ~/.git-completion.bash
fi
```
