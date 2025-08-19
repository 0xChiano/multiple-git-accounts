cd ~/.ssh

ssh-keygen -t rsa -C thechiano@gmail.com -f github-work
ssh-keygen -t rsa -C YOUR_GIT_EMAIL_HERE -f github-personal

ssh-add --apple-use-keychain ~/.ssh/github-personal

ssh-add --apple-use-keychain ~/.ssh/github-work

pbcopy < ~/.ssh/github-personal.pub

pbcopy < ~/.ssh/github-work.pub

open -e ~/.ssh/config

# Your Personal GitHub Account
Host github.com-personal
    HostName github.com
    User git
    IdentityFile ~/.ssh/github-personal

# Your Work GitHub Account
Host github.com-work
    HostName github.com
    User git
    IdentityFile ~/.ssh/github-work


git config --global user.name YOUR_GIT_USERNAME_HERE

git config --global user.email YOUR_GIT_EMAIL_HERE

git clone git@github.com-personal:yourusername/cool-project.git


git config user.email "you@example.com"

git config user.name "Your Name"





