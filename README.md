# Git Started

## Set up SSH keys

```sh
ssh-keygen -t rsa -b 4096 -C "your_github_email@address.com"
```

Start the ssh-agent in the background.

```sh
eval "$(ssh-agent -s)" # Agent pid 10164
```

Create SSH config file

```sh
touch ~/.ssh/config
```

Edit SSH config file

```
Host *
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_rsa
```

Add SSH private key to the ssh-agent, and store passphrase in the keychain

```sh
ssh-add -K ~/.ssh/id_rsa
```

Stop the ssh-agent in the background

```sh
kill 10164 # or whatever `Agent pid` that was generated
```

## Copy SSH keys to GitHub

1. Open terminal
2. Copy the SSH key to your clipboard `pbcopy < ~/.ssh/id_rsa.pub`
3. Navigate to https://github.com/
4. Click on profile photo, and select "Settings" from the menu (top right corner of the screen)
5. On the settings-page, click on the "SSH and GPG keys" link (right side of the screen)
6. On the ssh-and-gpg-keys page, click on the "New SSH key" button (right side of the screen)

## Create repository

1. Navigate to https://github.com/
2. Click on the "New" button (left side of the screen, next to the "Repositories" heading)
3. On the create-new-repository page, enter a "Repository name", e.g. git-started
4. Click the "Create repository" button (bottom of the screen)

## Clone and configure repository

```sh
git clone git@github.com:<user>/<repository>.git # e.g. git clone git@github.com:spiderwebrobot/git-started.git
```

Specify how to reconcile divergent branches

```sh
git config pull.rebase false
```

## Create a feature-branch

Get the latest changes from the `main` branch

```
git checkout main
git pull
```

Switch to a feature-branch

```
git checkout -b feature/initial-updates
```

## Merge changes to `main` branch

Add and commit changes

```sh
git add .
git commit
```

Switch back to `main` branch to get latest changes again

```
git checkout main
git pull
```

Switch back to feature-branch to merge in changes from `main` branch

```
git checkout feature/initial-updates
git merge master
```

Switch back to `main` branch to merge feature-branch

```
git checkout main
git pull
git merge feature/initial-updates
```
