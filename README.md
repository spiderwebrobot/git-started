# Git Started

* [Prerequisites](#prerequisites)
* [Repository setup](#repository-setup)
* [Workflow](#workflow)
* [Resources](#resources)

## Prerequisites

### Set up SSH keys

1. Open a terminal and create a new authentication key pair, e.g...
   ```sh
   ssh-keygen -t rsa -b 4096 -C "your_github_email@address.com"
   ```
2. Start the ssh-agent in the background (which will generate a process ID, e.g. `Agent pid 10164`)
   ```sh
   eval "$(ssh-agent -s)"
   ```
3. Create an SSH config file
   ```sh
   touch ~/.ssh/config
   ```
4. Edit the SSH config file
   ```
   Host *
     AddKeysToAgent yes
     UseKeychain yes
     IdentityFile ~/.ssh/id_rsa
   ```
5. Add the SSH private key to the ssh-agent, and store the passphrase in the keychain
   ```sh
   ssh-add -K ~/.ssh/id_rsa
   ```
6. Stop the ssh-agent in the background
   ```sh
   kill 10164 # or whatever `Agent pid` that was generated
   ```

### Copy SSH keys to GitHub

1. Open a terminal
2. Copy the SSH key to your clipboard `pbcopy < ~/.ssh/id_rsa.pub`
3. Navigate to https://github.com/
4. Click on profile photo, and select "Settings" from the menu (top right corner of the screen)
5. On the settings-page, click on the "SSH and GPG keys" link (right side of the screen)
6. On the ssh-and-gpg-keys page, click on the "New SSH key" button (right side of the screen)

## Repository setup

### Create the repository

1. Open a browser
2. Navigate to https://github.com/
3. Click on the "New" button (left side of the screen, next to the "Repositories" heading)
4. On the create-new-repository page, enter a "Repository name", e.g. git-started
5. Click the "Create repository" button (bottom of the screen)

### Clone and configure the repository

Open a terminal and...

```sh
git clone git@github.com:[user]/[repository].git # e.g. git clone git@github.com:spiderwebrobot/git-started.git
```

Navigate into the repository

```sh
cd [repository] # e.g. cd git-started
```

Specify how to reconcile divergent branches

```sh
git config pull.rebase false
```

Push the current branch to update a branch with the same name

```sh
git config push.default current
```

Establish your identity

```sh
git config user.name "Your Name" && git config user.email your@address.com
```

## Workflow

### Create a feature-branch

Open a terminal and...

```sh
git checkout main && git pull
```

Create and switch to a feature-branch

```sh
git checkout -b feature/initial-updates
```

Open a code-editor and make changes to the feature-branch

### Add and commit the feature-branch changes

```sh
git add . && git commit
```

### Sync the feature-branch with the main-branch

Open a terminal and...

```sh
git checkout main && git pull
```

Switch to the feature-branch, and merge changes from the main-branch

```sh
git checkout feature/initial-updates && git merge main
```

### Create pull-request for the feature-branch

Push the feature-branch changes

1. Open a terminal
2. Make sure the feature-branch changes are in sync with the main-branch (see instructions above)
3. Push the feature-branch `git push`

After pushing the feature-branch...

1. Open a browser
2. Navigate to the "Your branches" page, e.g. `https://github.com/spiderwebrobot/git-started/branches/yours`
3. On the "Your branches" page, click on the respective "New pull request" button
4. On the "Open a pull request" page, click on the "Create pull request" button

### Deploy the feature-branch changes

Merge the feature-branch changes into the main-branch

1. Open a browser
2. Navigate to the "Pull requests" page, e.g. `https://github.com/spiderwebrobot/git-started/pulls`
3. On the "Pull requests" page, click on the feature-branch to be merged
4. Select "Squash and merge" from the "Merge pull request" dropdown menu (if not already selected)
5. Click on the "Squash and merge" button
6. Click on the "Confirm squash and merge" button
7. Click on the "Delete branch" button

## Resources

* [Generate a New SSH Key](https://www.ssh.com/ssh/keygen/)
* [Generating a new SSH key and adding it to the ssh-agent](https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
* [Adding a new SSH key to your GitHub account](https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/adding-a-new-ssh-key-to-your-github-account)
* [GitHub Git Cheat Sheet](https://training.github.com/downloads/github-git-cheat-sheet/)
* [Mastering Markdown](https://guides.github.com/features/mastering-markdown/)
* [Git: How to configure git to push only your current branch](https://makandracards.com/makandra/8039-git-how-to-configure-git-to-push-only-your-current-branch)
