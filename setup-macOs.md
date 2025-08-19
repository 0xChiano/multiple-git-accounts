# Setting up Multiple GitHub Accounts on macOS using SSH

This guide will help you configure multiple GitHub accounts (personal and work) on macOS using SSH keys.

## Prerequisites

- macOS with Terminal access
- Git installed
- GitHub accounts (personal and work)

## Step 1: Generate SSH Keys

Navigate to the SSH directory and generate separate keys for each account:

```bash
cd ~/.ssh
ssh-keygen -t rsa -C "YOUR_PERSONAL_EMAIL@example.com" -f github-personal
ssh-keygen -t rsa -C "YOUR_WORK_EMAIL@example.com" -f github-work
```

## Step 2: Add Keys to SSH Agent

Add both keys to the SSH agent with keychain integration:

```bash
ssh-add --apple-use-keychain ~/.ssh/github-personal
ssh-add --apple-use-keychain ~/.ssh/github-work
```

## Step 3: Copy Public Keys

Copy the public keys to add them to your GitHub accounts:

```bash
# Copy personal key
pbcopy < ~/.ssh/github-personal.pub
# Go to GitHub (personal account) → Settings → SSH Keys → Add the key

# Copy work key  
pbcopy < ~/.ssh/github-work.pub
# Go to GitHub (work account) → Settings → SSH Keys → Add the key
```

## Step 4: Configure SSH Config File

Open the SSH config file:

```bash
open -e ~/.ssh/config
```

Add the following configuration:

```
# Personal GitHub Account
Host github.com-personal
    HostName github.com
    User git
    IdentityFile ~/.ssh/github-personal

# Work GitHub Account
Host github.com-work
    HostName github.com
    User git
    IdentityFile ~/.ssh/github-work
```

## Step 5: Set Global Git Configuration (Optional)

Set your default Git configuration (usually your personal account):

```bash
git config --global user.name "YOUR_PERSONAL_USERNAME"
git config --global user.email "YOUR_PERSONAL_EMAIL@example.com"
```

## Step 6: Clone and Configure Repositories

### For Personal Repositories:
```bash
git clone git@github.com-personal:yourusername/your-repo.git
cd your-repo
git config user.email "YOUR_PERSONAL_EMAIL@example.com"
git config user.name "YOUR_PERSONAL_USERNAME"
```

### For Work Repositories:
```bash
git clone git@github.com-work:companyusername/work-repo.git
cd work-repo
git config user.email "YOUR_WORK_EMAIL@example.com"
git config user.name "YOUR_WORK_USERNAME"
```

## Important Notes

- Replace all placeholder values (`YOUR_*_EMAIL@example.com`, `yourusername`, etc.) with your actual information
- The SSH config hosts (`github.com-personal`, `github.com-work`) are custom aliases you'll use in your git URLs
- Always set the correct user email and name for each repository to ensure proper commit attribution
- You can verify your SSH connection with: `ssh -T git@github.com-personal` or `ssh -T git@github.com-work`

## Troubleshooting

If you encounter issues:
1. Check if your keys are loaded: `ssh-add -l`
2. Test SSH connection: `ssh -T git@github.com-personal`
3. Verify your SSH config file syntax
4. Ensure the correct email is associated with each repository
