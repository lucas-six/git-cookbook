# Git Server (SSH Protocal)

## Local Machine

### Export Bare Repository

```bash
mkdir <project>.git
cd <project>.git
git init --bare

git clone --bare <project-dir> <git-repo>.git
```

### Put Bare Repository on Server

```bash
scp -r <git-repo>.git <user>@<git-server>:/<path-to-git-repo>
```

## Server

## Recipe

```bash
sudo adduer git
sudo passwd git
sudo chown git:git  /<path-to-git-repo>
```

```bash
sudo adduser <user>
sudo passwd <user>
gpasswd -a <user> git
```

## References

- [Pro Git v2 - 4.1 Git on the Server - The Protocols](https://git-scm.com/book/en/v2/Git-on-the-Server-The-Protocols)
