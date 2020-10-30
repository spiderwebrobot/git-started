# Git Started

## Initial setup

### Set up SSH keys

```sh
ssh-keygen -t rsa -b 4096 -C "your_github_email@address.com"
```

Start the ssh-agent in the background (which will generate an agent process ID, e.g. `Agent pid 10164`)

```sh
eval "$(ssh-agent -s)"
```

Create an SSH config file

```sh
touch ~/.ssh/config
```

Edit the SSH config file

```
Host *
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_rsa
```

Add the SSH private key to the ssh-agent, and store the passphrase in the keychain

```sh
ssh-add -K ~/.ssh/id_rsa
```

Stop the ssh-agent in the background

```sh
kill 10164 # or whatever `Agent pid` that was generated
```

### Copy SSH keys to GitHub

1. Open terminal
2. Copy the SSH key to your clipboard `pbcopy < ~/.ssh/id_rsa.pub`
3. Navigate to https://github.com/
4. Click on profile photo, and select "Settings" from the menu (top right corner of the screen)
5. On the settings-page, click on the "SSH and GPG keys" link (right side of the screen)
6. On the ssh-and-gpg-keys page, click on the "New SSH key" button (right side of the screen)

## Repository setup

### Create the repository

1. Navigate to https://github.com/
2. Click on the "New" button (left side of the screen, next to the "Repositories" heading)
3. On the create-new-repository page, enter a "Repository name", e.g. git-started
4. Click the "Create repository" button (bottom of the screen)

### Clone and configure the repository

```sh
git clone git@github.com:[user]/[repository].git # e.g. git clone git@github.com:spiderwebrobot/git-started.git
```

Specify how to reconcile divergent branches

```sh
git config pull.rebase false
```

Establish your identity

```sh
git config user.name "Your Name"
git config user.email your@address.com
```

## Workflow

### Create a feature-branch

Get the latest changes from the main-branch

```sh
git checkout main
git pull
```

Create and switch to a feature-branch

```sh
git checkout -b feature/initial-updates
```

### Add and commit the feature-branch changes

```sh
git add .
git commit
```

### Sync the feature-branch with the main-branch

Switch to main-branch to get latest changes

```sh
git checkout main
git pull
```

Switch to feature-branch, and merge changes from main-branch

```sh
git checkout feature/initial-updates
git merge main
```

### Create pull-request for the feature-branch

Make sure the feature-branch changes are in sync with the main-branch before proceeding (see instructions above)

```sh
git push --set-upstream origin feature/initial-updates
```

1. Copy and paste the pull-request URL into browser `https://github.com/[user]/[repository]/pull/new/feature/initial-updates`
2. I think something goes here?...
3. Navigate to the newly created pull-request e.g. `https://github.com/[user]/[repository]/pull/1`

### Publish the feature-branch changes

Merge the feature-branch changes into the main-branch

1. Select "Squash and merge" from the "Merge pull request" dropdown menu
2. Click on the "Squash and merge" button
3. Click on the "Confirm squash and merge" button
4. Click on the "Delete branch" button

## Resources

* [Generating a new SSH key and adding it to the ssh-agent](https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
* [Adding a new SSH key to your GitHub account](https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/adding-a-new-ssh-key-to-your-github-account)
* [GitHub Git Cheat Sheet](https://training.github.com/downloads/github-git-cheat-sheet/)
