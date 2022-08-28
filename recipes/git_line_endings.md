# Git Handling Line Endings (CRLF)

## Line Endings Issues

If you’re programming on Windows and working with people who are not (or vice-versa),
you’ll probably run into **line-ending issues** at some point.
This is because Windows uses *both a carriage-return character and a linefeed character* (**CRLF**)
for newlines in its files,
whereas Mac, Linux, Unix systems use only the *linefeed character* (**LF**).
This is a subtle but incredibly annoying fact of cross-platform work;
many editors on Windows silently replace existing LF-style line endings with CRLF,
or insert both line-ending characters when the user hits the enter key.

On Windows:

```bash
$ git add somefile
warning: LF will be replaced by CRLF in somefile.
The file will have its original line endings in your working directory.
```

## Solution

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
You can tell Git to convert *CRLF* to *LF* on commit but not the other way around
by setting *`core.autocrlf`* to **`input`**:

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

**Note**: `core.autocrlf` will not affect content which is already in the repository.
If you've committed something with CRLF endings previously, they'll stay that way.
This is a very good reason to avoid depending on `core.autocrlf`;
if one user doesn't have it set, they can get content with CRLF endings into the repo,
and it'll stick around.

## CRLF Safety Check

CRLF conversion bears a slight chance of corrupting data. When *`core.autocrlf`* is enabled,
Git will convert CRLF to LF during commit and LF to CRLF during checkout.
A file that contains a mixture of LF and CRLF before the commit cannot be recreated by Git.
For *text files* this is the right thing to do:
it corrects line endings such that we have only LF line endings in the repository.
But for *binary files* that are accidentally classified as text the conversion can corrupt data.

Unfortunately, the desired effect of cleaning up text files with mixed line endings
and the undesired effect of corrupting binary files cannot be distinguished.
In both cases CRLFs are removed in an **irreversible way**.
For text files this is the right thing to do because CRLFs are line endings,
while for binary files converting CRLFs **corrupts data**.

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

The variable can be set to *`warn`*, in which case Git will only warn about an irreversible conversion
but continue the operation.

```bash
$ git config core.safecrlf warn

$ git add somefile
warn: CRLF would be replaced by LF in somefile.
```

## Per-repository Settings: Git Attributes

Optionally, you can configure a **`.gitattributes`** file
to manage how Git reads line endings in a specific repository.
When you commit this file to a repository, it overrides the *`core.autocrlf`* setting
for all repository contributors.
This ensures consistent behavior for all users, regardless of their Git settings and environment.

The `.gitattributes` file must be created in the *root* of the repository
and committed like any other file.

A `.gitattributes` file looks like a table with two columns:

- On the left is the file name for Git to match.
- On the right is the line ending configuration that Git should use for those files.

### `.gitattributes` Example

Here's an example `.gitattributes` file. You can use it as a template for your repositories:

```ini
# Set the default behavior, in case people don't have core.autocrlf set.
* text=auto

# Explicitly declare text files you want to always be normalized and converted
# to native line endings on checkout.
*.c text
*.h text

# Declare files that will always have CRLF line endings on checkout.
*.sln text eol=crlf

# Denote all files that are truly binary and should not be modified.
*.png binary
*.jpg binary
```

We'll go over some possible settings below.

- `text=auto` Git will handle the files in whatever way it thinks is best. This is a good default option.

- `text eol=crlf` Git will always convert line endings to CRLF on checkout.
You should use this for files that must keep CRLF endings, even on OSX or Linux.

- `text eol=lf` Git will always convert line endings to LF on checkout.
You should use this for files that must keep LF endings, even on Windows.

- `binary` Git will understand that the files specified are not text,
and it should not try to change them.
The `binary` setting is also an alias for `-text -diff`.

## `core.eol`

Sets the line ending type to use in the working directory for files that are marked as text.
Alternatives are **`lf`**, **`crlf`** and **`native`**, which uses the platform’s native line ending.
The default value is *`native`*.

```bash
git config core.eol lf      # LF
git config core.eol crlf    # CRLF
git config core.eol native  # platform (default)
```
