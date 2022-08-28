# Git URL

Git supports **ssh**, **git**, and **http[s]** protocols.

The following syntaxes may be used with them:

- *`ssh://[user@]host[:port]/path/to/repo.git/`*

- *`git://host[:port]/path/to/repo.git/`*

- *`http[s]://host[:port]/path/to/repo.git/`*

The native transport (i.e. `git://URL)` does no authentication
and should be used with caution on unsecured networks.

An alternative **scp**-like syntax may also be used with the ssh protocol:

```plaintext
[user@]host:path/to/repo.git/
```

## `~` Expansion

The *ssh* and *git* protocols additionally support `~username` expansion:

- *`ssh://[user@]host[:port]/~[user]/path/to/repo.git/`*

- *`git://host[:port]/~[user]/path/to/repo.git/`*

- *`[user@]host:/~[user]/path/to/repo.git/`*

## Local Repositories

For local repositories, also supported by Git natively, the following syntaxes may be used:

- *`/path/to/repo.git/`*

- *`file:///path/to/repo.git/`*

These two syntaxes are mostly equivalent, except the former implies **`--local`** option.
