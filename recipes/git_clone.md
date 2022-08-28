# Git Clone

## Basic Clone

```bash
git clone https://github.com/leven-cn/git-cookbook.git
```

After the clone, a plain *`git fetch`* without arguments will update all the remote-tracking branches,
and a *`git pull`* without arguments will in addition merge the remote `master` or `main` branch
into the current `master` or `main` branch,
if any (this is untrue when "*`--single-branch`*" is given).

This default configuration is achieved by creating references to the remote branch heads under *`refs/remotes/origin`*
and by initializing *`remote.origin.url`* and *`remote.origin.fetch`* configuration variables.

More details about URL for Git to see [Git URL](https://leven-cn.github.io/git-cookbook/recipes/git_url).

## Examples

### Clone From Upstream

```bash
git clone https://github.com/leven-cn/git-cookbook.git git-cookbook

git clone <remote>:~/git-cookbook.git      # SSH: remote path on host "remote", ignore `ssh://`

git clone /home/<remote-user>/git-cookbook.git  # local path, ignore `file://`
```

## References

- [Git Homepage](https://git-scm.com "Git Homepage")
