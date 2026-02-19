# GitHub & SSH Cheatsheet

## SSH Key Setup

```bash
# Generate SSH key (no passphrase)
ssh-keygen -t ed25519 -C "your-email@example.com" -f ~/.ssh/id_keyname -N ""

# View public key (copy this to GitHub → Settings → SSH keys)
cat ~/.ssh/id_keyname.pub

# Test SSH connection to GitHub
ssh -T git@github.com
```

## Managing Multiple GitHub Accounts

### ~/.ssh/config

```
Host github-work
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_work

Host github-personal
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_personal
```

```bash
# Verify each account
ssh -T git@github-work
ssh -T git@github-personal

# Clone using the correct host alias
git clone git@github-personal:username/repo.git
git clone git@github-work:org/repo.git

# Fix remote URL on an existing repo
git remote set-url origin git@github-personal:username/repo.git
```

## Git Identity (per repo)

```bash
# Set commit identity for current repo only
git config user.name "Your Name"
git config user.email "your-email@example.com"

# Check current identity
git config user.name
git config user.email

# Check global identity
git config --global user.name
git config --global user.email
```

## SSH Key Permissions

```bash
# Keys should be 600 (read/write only by owner)
chmod 600 ~/.ssh/id_keyname

# Check permissions
ls -la ~/.ssh/id_keyname
```

## SSH Agent (only needed if you set a passphrase)

```bash
# Start agent
eval "$(ssh-agent -s)"

# Add key to agent (caches passphrase for the session)
ssh-add ~/.ssh/id_keyname

# List keys loaded in agent
ssh-add -l
```

## GitHub CLI

```bash
# Check which account is authenticated
gh auth status

# Login
gh auth login

# Create and clone a new repo
gh repo create repo-name --public --clone
```
