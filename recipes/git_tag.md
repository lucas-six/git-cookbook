# `git tag`

## Usage

```bash
git tag -a <tag> -m '<tag-comment>'      # e.g., git tag -a 'v0.1' -m 'v0.1 - Initial version'

git push --tag                           # Add remote tag
git push origin :refs/tags/<tag-name>    # Delete remote tag
```

## References

- [Git Documentation - `git tag`](https://git-scm.com/docs/git-tag)
