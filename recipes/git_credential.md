# Git Credential

## Cache in memory (temporarily)

```bash
git config credential.helper cache
```

default: `900` seconds.

Set number of seconds to cache credentials:

```bash
git config credential.helper 'cache --timeout=<seconds>'
```

## Store on disk (unencrypted)

**Warning**: Store your password in local host, ensure you are working in a secure environment.

```bash
git config --global credential.helper store
```

Default: `~/.git-credentials` and `$XDG_CONFIG_HOME/git/credentials`.

Use `<path>` to lookup and store credentials:

```bash
git config --global credential.helper 'store --file=<path>'
```

## macOS (KeyChain)

```bash
git config --global credential.helper osxkeychain
```

## Linux (Libsecret)

```bash
sudo apt install libsecret-1-dev
cd /usr/share/doc/git/contrib/credential/libsecret
sudo make
git config --global credential.helper /usr/share/doc/git/contrib/credential/libsecret/git-credential-libsecret
```

## References

- [git-credential Documentation](https://git-scm.com/docs/gitcredentials)
- [git-credential-cache Documentation](https://git-scm.com/docs/git-credential-cache)
- [git-credential-store Documentation](https://git-scm.com/docs/git-credential-store)
