# Git whitespace errors

By default, *trailing whitespaces* (including lines that consist *solely of whitespaces*)
and a space character that is immediately followed
by a tab character inside the initial indent of the line are considered **whitespace errors**.

Git, with setting **`core.whitespace`**, comes preset to detect and fix some whitespace issues.
It can look for six primary whitespace issues — three are enabled by default and can be turned off,
and three are disabled by default but can be activated.

The three that are *turned on* by default:

- **`blank-at-eol`**, which looks for spaces at *the end of a line* (*EOL*);
- **`blank-at-eof`**, which notices blank lines at *the end of a file* (*EOF*);
- **`space-before-tab`**, which looks for spaces before tabs at the beginning of a line.

**`trailing-space`** being a short-hand to cover both *`blank-at-eol`* and *`blank-at-eof`*.

The three that are *disabled* by default but can be turned on:

- **`indent-with-non-tab`**, which looks for lines that begin with spaces instead of tabs
(and is controlled by the *`tabwidth`* option);
- **`tab-in-indent`**, which watches for tabs in the indentation portion of a line;
- **`cr-at-eol`**, which tells Git that *carriage returns* (CR: *`\r`*) at the end of lines are OK.

You can disable an option by prepending a **`-`** in front of its name,
or use the default value by leaving it out of the setting string entirely.

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

Git will detect these issues when you run a *`git diff`* command and try to color them
so you can possibly fix them before you commit.

## `git apply --whitespace` / `git config apply.whitespace`

It will also use these values to help you when you apply patches with *`git apply`*.
When you’re applying patches, you can ask Git to warn or error you
if it’s applying patches with the specified whitespace issues:

```bash
git apply --whitespace=warn <patch>
git apply --whitespace=error <patch>      # a few such errors
git apply --whitespace=error-all <patch>  # all errors
```

Or

```bash
git config apply.whitespace warn
git config apply.whitespace error      # a few such errors
git config apply.whitespace error-all  # all errors
```

Or you can have Git try to automatically fix the issue before applying the patch:

```bash
git apply --whitespace=fix <patch>
```

Or

```bash
git config apply.whitespace fix
```

Or turning off the warning:

```bash
git apply --whitespace=nowarn <patch>
```

Or

```bash
git config apply.whitespace nowarn
```

## `git rebase`

These options apply to the *`git rebase`* command as well.
If you’ve committed whitespace issues but haven’t yet pushed upstream,
you can have Git automatically fix whitespace issues as it’s rewriting the patches:

```bash
git rebase --whitespace=fix
```

More details about *`core.whitespace`* configuration please refer to [Git Configuration](https://leven-cn.github.io/git-cookbook/recipes/git_config).
