# Git Configuration

## Scope

```bash
git config --system <name> [<value>]
git config --global <name> [<value>]
git config --local <name> [<value>]
git config --worktree <name> [<value>]
git config --file <config-file> <name> [<value>]
```

- **`--system`** system-wide, for all users in the system
- **`--global`** user-wide, for current user
- **`--local`** for current repository (by default)
- **`--worktree`** for current working tree
- **`--file`**, **`-f`** for specified file `config-file`

## User Info

```bash
git config --global user.name 'Your Name'
git config --global user.email your@email.com  # Your working email, just as GitHub registered email
```

## Show Current Configuration

```bash
git config --list  # all configs

git config <name>  # specified config
```

## Editor: `core.editor`

By default, Git uses whatever you’ve set as your default text editor
via one of the shell environment variables *`VISUAL`* or *`EDITOR`*,
or else falls back to the *`vi`* editor to create and edit your commit and tag messages.
To change that default to something else, you can use the **`core.editor`** setting.

### Command Line or Terminal

Use *Vim*:

```bash
git config --global core.editor vim
```

Use *Emacs*:

```bash
git config --global core.editor emacs
```

### GUI

Use *gVim*:

```bash
git config --global core.editor "gvim --nofork"
```

Use *VS Code*:

```bash
git config --global core.editor "code --wait"
```

## Pager `core.pager`

Determine which pager is used when Git pages output such as `git log` and `git diff`.

Use *less*, by default.

```bash
git config --global core.pager less
```

Use *more*:

```bash
git config --global core.pager more
```

You can turn it off by setting it to a blank string:

```bash
git config --global core.pager ''
```

If you run that, Git will page the entire output of all commands, no matter how long they are.

## External Diff Tools

### Command Line or Terminal: `diff.tool`

Controls which diff tool is used by *`git difftool`*.

Generally *Vim* is installed on Linux and Macos by default,
so **`vimdiff`** (same as *`vim -d`*) could be used:

```bash
git config --global diff.tool vimdiff
```

*gVim* (**`gvimdiff`**, same as *`gvim -d --nofork`*) could be used on Linux:

```bash
git config --global diff.tool gvimdiff
git config --global difftool.prompt false
```

*WinMerge* could be used on Windows:

```bash
git config --global diff.tool winmerge
```

*VS Code* could be used on any of Macos, Linux, and Windows:

```bash
git config --global diff.tool "vscode"
git config --global difftool.vscode.cmd 'code --wait --diff $LOCAL $REMOTE'
```

### GUI `diff.guitool`

Controls which diff tool is used by *`git difftool --gui`* or `git difftool -g`.

*gVim* (**`gvimdiff`**, same as *`gvim -d --nofork`*) could be used on Linux:

```bash
git config --global diff.guitool gvimdiff
git config --global guitool.prompt false
```

*WinMerge* could be used on Windows:

```bash
git config --global diff.guitool winmerge
```

## Color: `color.*`

Use variable **`color.ui`** to determine the *default* value for variables
such as *`color.status`*, *`color.diff`*, *`color.transport`*, *`color.remote`*, *`color.showBranch`*,
and *`color.grep`* that control the use of color per command family.

## Line Endings Issues

### `core.autocrlf`

Git can handle this by auto-converting *CRLF* line endings into *LF*
when you add a file to the index (`git add`), and vice versa when it checks out code onto your filesystem.

If you’re on a **Windows** machine, set the setting *`core.autocrlf`* to **`true`** —
this converts *LF* endings into *CRLF* when you check out code:

```bash
# Checkout Windows-style, commit Unix-style line endings
git config --global core.autocrlf true
```

If you’re on a **Linux**, **UNIX** or **Mac** system that uses *LF* line endings,
then you don’t want Git to automatically convert them when you check out files;
however, if a file with *CRLF* endings accidentally gets introduced, then you may want Git to fix it.
You can tell Git to convert *CRLF* to *LF* on commit
but not the other way around by setting *`core.autocrlf`* to **`input`**:

```bash
# Checkout as-is, commit Unix-style line endings
git config --global core.autocrlf input
```

If you’re a Windows programmer doing a **Windows-only** project, then you can turn off this functionality,
recording the *carriage returns* (*CR*) in the repository by setting the config value to **`false`**：

```bash
# Checkout as-is, commit as-is
git config core.autocrlf false
```

!!! warn "Note"
    `core.autocrlf` will not affect content which is already in the repository.
    If you've committed something with CRLF endings previously, they'll stay that way.
    This is a very good reason to avoid depending on `core.autocrlf`;
    if one user doesn't have it set, they can get content with CRLF endings into the repo,
    and it'll stick around.

### `core.safecrlf`

**`core.safecrlf`** is basically just a way to
make sure you don't irreversably perform CRLF conversion on a **binary file**.

If *`true`*, makes Git check if converting CRLF is reversible *when end-of-line conversion*
(*`core.autocrlf`*) is active (*`true`* or *`input`*).
Git will verify if a command modifies a file in the work tree either directly or indirectly.
For example, committing a file followed by checking out the same file should yield the original file
in the work tree.
If this is not the case for the current setting of `core.autocrlf`, Git will reject the file:

```bash
$ git add somefile
fatal: CRLF would be replaced by LF in somefile.
```

The variable can be set to *`warn`*,
in which case Git will only warn about an irreversible conversion but continue the operation.

```bash
$ git config core.safecrlf warn

$ git add somefile
warn: CRLF would be replaced by LF in somefile.
```

### `core.eol`

Sets the line ending type to use in the working directory for files that are marked as text.
Alternatives are **`lf`**, **`crlf`** and **`native`**, which uses the platform’s native line ending.
The default value is *`native`*.

```bash
git config core.eol lf      # LF
git config core.eol crlf    # CRLF
git config core.eol native  # platform (default)
```

## Whitespace Error: `core.whitespace` / `apply.whitespace`

A comma separated list of common **whitespace problems** to notice. (See [[Git whitespace errors]])

*`git diff`* will use *`color.diff.whitespace`* to highlight them,
and *`git apply --whitespace=error`* will consider them as errors.
You can prefix *`-`* to disable any of them (e.g. `-trailing-space`):

- **`blank-at-eol`** treats trailing whitespaces at *the end of the line* (*EOL*) as an error
(enabled by default).

- **`space-before-tab`** treats a space character that appears immediately before a tab character
in the initial indent part of the line as an error (enabled by default).

- **`indent-with-non-tab`** treats a line that is indented with space characters
instead of the equivalent tabs as an error (not enabled by default).

- **`tab-in-indent`** treats a tab character in the initial indent part of the line as an error
(not enabled by default).

- **`blank-at-eof`** treats blank lines added at *the end of file* (*EOF*) as an error (enabled by default).

- **`trailing-space`** is a short-hand to cover both *`blank-at-eol`* and *`blank-at-eof`*.

- **`cr-at-eol`** treats a *carriage-return* (*CR*: *`\r`*) at the end of line as part of the line terminator,
i.e. with it, `trailing-space` does not trigger if the character before such a carriage-return
is not a whitespace (not enabled by default).

- **`tabwidth=<n>`** tells how many character positions a tab occupies;
this is relevant for *`indent-with-non-tab`* and when Git fixes *`tab-in-indent`* errors.
The default tab width is *8*. Allowed values are *1* to *63*.

For example, if you want all but *`space-before-tab`* to be set, you can do this:

```bash
git config --global core.whitespace \
    trailing-space,-space-before-tab,indent-with-non-tab,tab-in-indent,cr-at-eol
```

Or you can specify the customizing part only:

```bash
git config --global core.whitespace \
    -space-before-tab,indent-with-non-tab,tab-in-indent,cr-at-eol
```

## Push Default Action

```bash
git config --global push.default simple
```

- **`simple`**: pushes the current branch with the same name on the remote. (default)
- **`upstream`**: push the current branch back to the branch
whose changes are usually integrated into the current branch. (for central workflow)
- **`current`**: push the current branch to update a branch with the same name on the receiving end.
(for central and non-centra workflows)
- **`nothing`**: do not push anything (error out) unless a refspec is given.
This is primarily meant for people who want to avoid mistakes by always being explicit.
- **`matching`**: push all branches having the same name on both ends.

## Example

```bash
sudo git config --system core.editor vim
sudo git config --system diff.tool vimdiff
sudo git config --system help.autocorrect 1
sudo git config --system core.filemode true
sudo git config --system gui.encoding utf-8

git config --global user.name 'Your Name'
git config --global user.email your@email.com
git config --global core.editor "code --wait"
git config --global core.autocrlf input
git config --global diff.tool "vscode"
git config --global difftool.vscode.cmd 'code --wait --diff $LOCAL $REMOTE'
git config --global push.default simple
```

## References

- [Git Documentation - `git config`](https://git-scm.com/docs/git-config)
