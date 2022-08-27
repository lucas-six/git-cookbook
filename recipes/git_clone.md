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

## Git URL

Git supports **ssh**, **git**, **http**, and **https** protocols.

The native transport (i.e. `git://URL)` does no authentication
and should be used with caution on unsecured networks.

The following syntaxes may be used with them:

- *`ssh://[user@]host[:port]/path/to/repo.git/`*

- *`git://host[:port]/path/to/repo.git/`*

- *`http[s]://host[:port]/path/to/repo.git/`*

An alternative **scp**-like syntax may also be used with the ssh protocol:

*`[user@]host:path/to/repo.git/`*

The *ssh* and *git* protocols additionally support `~username` expansion:

- *`ssh://[user@]host[:port]/~[user]/path/to/repo.git/`*

- *`git://host[:port]/~[user]/path/to/repo.git/`*

- *`[user@]host:/~[user]/path/to/repo.git/`*

### Local Repositories

For local repositories, also supported by Git natively, the following syntaxes may be used:

- *`/path/to/repo.git/`*

- *`file:///path/to/repo.git/`*

These two syntaxes are mostly equivalent, except the former implies **`--local`** option.

## Examples

### Clone From Upstream

```bash
git clone https://github.com/leven-cn/git-cookbook.git git-cookbook

git clone <remote>:~/git-cookbook.git      # SSH: remote path on host "remote", ignore `ssh://`

git clone /home/<remote-user>/git-cookbook.git  # local path, ignore `file://`
```

## References

- [Git Homepage](https://git-scm.com "Git Homepage")
