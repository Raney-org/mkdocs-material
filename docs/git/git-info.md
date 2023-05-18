---
tags:
  - GIT
---

# Git Info

## Where to Start

So I've been bothering old Chat-GPT with millions of questions lately. Its pretty great. I'll try to keep this legible, but no guarantees. I was all over the place with my questions. I'll probably refactor this a hundred times before I'm satisfied with it, but here we go!

## how do you authenticate an ssh key with github

To authenticate an `SSH` key with `GitHub`, follow these steps:

1. Check for existing SSH keys:
    First, check if you already have an SSH key pair. Open a terminal (or Git Bash on Windows) and run the following command:

    ``` sh
    ls -al ~/.ssh
    ```

    Look for a pair of files named `id_rsa` (private key) and `id_rsa.pub` (public key). If you don't have these files, proceed to step 2.

2. Generate a new `SSH` key pair:
    Run the following command, replacing `"youremail@example.com"` with your GitHub email address:

    ``` sh
    ssh-keygen -t rsa -b 4096 -C "youremail@example.com"
    ```

    Press `Enter` to accept the default file location. You can set a passphrase for added security, but it's optional.

3. Add the `SSH` key to the `ssh-agent`:
    Start the ssh-agent in the background:

      - On `macOS` and `Linux`:

    ``` sh
    eval "$(ssh-agent -s)"
    ```

      - On `Windows` (Git Bash):

    ``` sh
    eval $(ssh-agent -s)
    ```

    Add the private `SSH` key to the `ssh-agent`:

    ``` sh
    ssh-add ~/.ssh/id_rsa
    ```

4. Add the public SSH key to your GitHub account:
    Copy the contents of the public key file. You can use the following command to output the contents and copy them to your clipboard:

      - On `macOS`:

    ``` sh
    pbcopy < ~/.ssh/id_rsa.pub
    ```

      - On `Linux` (with xclip installed):

    ``` sh
    xclip -sel clip < ~/.ssh/id_rsa.pub
    ```

     - On `Windows` (Git Bash):

    ``` sh
    clip < ~/.ssh/id_rsa.pub
    ```

    Now, go to GitHub and follow these steps:

     - Click on your profile picture in the upper-right corner and select `"Settings."`
     - In the left sidebar, click on `"SSH and GPG keys."`
     - Click the `"New SSH key"` button.
     - Enter a title for the key (e.g., `"My Laptop"`).
     - Paste the copied public key into the `"Key"` field.
     - Click the `"Add SSH key"` button.

5. Test the SSH connection:
Run the following command to test the SSH connection to GitHub:

``` sh
ssh -T git@github.com
```

You should see a message like `"Hi username! You've successfully authenticated..."`. If you encounter any issues, refer to the [GitHub SSH troubleshooting guide]

[GitHub SSH troubleshooting guide]: https://docs.github.com/en/authentication/troubleshooting-ssh

## How Do You Change a Local GitHub Repo From Using SSH to HTTPS

To change a local GitHub repository from using SSH to HTTPS, follow these steps:

1. Open a terminal (or Git Bash on Windows) and navigate to your local repository using the cd command:

    ``` sh
    cd path/to/your/repo
    ```

2. Check the current remote URL by running:

    ``` sh
    git remote -v
    ```

    This will display the remote URLs for fetching and pushing, which are currently using the SSH protocol (e.g., `git@github.com:username/repo.git`).

3. Change the remote URL from SSH to HTTPS:

    Find the HTTPS URL of your repository on GitHub by going to your repository page, clicking the green "Code" button, and selecting the "HTTPS" option. The URL will look like this: `https://github.com/username/repo.git`.

    Now, update the remote URL in your local repository by running:

    ``` sh
    git remote set-url origin https://github.com/username/repo.git
    ```

    Replace `https://github.com/username/repo.git` with the actual HTTPS URL you found on GitHub.

4. Verify the change:

    Run `#!shell git remote -v` again to check if the remote URLs for fetching and pushing have been updated to the HTTPS protocol.

    Now, your local GitHub repository is using HTTPS instead of SSH for communication. Keep in mind that you might be prompted to enter your GitHub username and password or personal access token when you push or pull changes.

## How do I set up VS Code to Commmit Everything as a Bot? and if I Wanted to Commit it as a Bot With a `GPG` Key, How Would I Do That?

To commit changes in VS Code as a bot, you need to configure Git with the bot's name and email address. Additionally, if you want to sign commits with a GPG key, you need to set up GPG for the bot and configure Git to use it.

Here's a step-by-step guide:

1. Configure Git with the bot's name and email address:[^1]

    Open the integrated terminal in VS Code and run the following commands:

    ```bash
    git config --global user.name "Your Bot Name"
    git config --global user.email "your-bot-email@example.com"
    ```

    Replace "Your Bot Name" and "`your-bot-email@example.com`" with the actual bot name and email address.

2. Set up GPG for the bot:

First, make sure you have GPG installed on your system. If you don't have it installed, you can download it from [GnuPG's official website].

Next, open the integrated terminal in VS Code and generate a new GPG key for the bot:

```bash
gpg --gen-key
```

Follow the prompts to create a new key. Make sure to use the bot's email address when asked for the user ID.

1. Configure Git to use the GPG key:

After generating the GPG key, list your GPG keys to get the key ID:

```bash
gpg --list-secret-keys --keyid-format LONG
```

Look for the line starting with `sec` and copy the key ID (the part after the `/` and before the date).

Now, configure Git to use this GPG key:

```bash
git config --global user.signingkey YOUR_KEY_ID
```

Replace `YOUR_KEY_ID` with the actual key ID you just copied.

1. Configure Git to sign all commits automatically:

To sign all commits automatically, run the following command:[^2]

[^2]: Keep in mind, this will make every commit to every repo you commit to use this.

```bash
git config --global commit.gpgsign true
```

Now, when you commit changes in VS Code, they will be committed as the configured bot and signed with the GPG key.

1. Add the GPG public key to your GitHub account:

To show the "Verified" badge on your commits on GitHub, you need to add the GPG public key to your GitHub account.

First, export the public key:

```bash
gpg --armor --export your-bot-email@example.com
```

Replace `your-bot-email@example.com` with the bot's email address. This command will output the public key in the terminal.

Copy the public key, including the lines `-----BEGIN PGP PUBLIC KEY BLOCK-----` and `-----END PGP PUBLIC KEY BLOCK-----`.

Then, go to your GitHub account settings, navigate to the "SSH and GPG keys" section, click on "New GPG key," and paste the public key. Click "Add GPG Key"

???+ note
    I went and stopped the illustrious chat bot right there. I'd had enough. You see, I only wanted this to work on/in one single github repo, not across any others that I contribute to, as I help with docs in another org that isn't associated with me and of which I am not a member. Because they are mean. But, I digress.

### I don't want to do this globally, just for my "raney-org/mkdocs-materials" github repo. I want to use my normal username and email for other repos

In that case, you can set the Git configuration and GPG signing on a per-repository basis. Here's how to do that for your specific repository:

1. Open the "raney-org/mkdocs-materials" repository in VS Code.

2. Open the integrated terminal in VS Code.

3. Configure Git with the bot's name and email address for this specific repository:[^3]

4. Configure Git to use the GPG key for this specific repository:

```bash
git config user.signingkey YOUR_KEY_ID
```

Replace `YOUR_KEY_ID` with the actual key ID of the GPG key you want to use for this repository.

5. Configure Git to sign all commits automatically for this specific repository:

   ```bash
   git config commit.gpgsign true
   ```

Now, when you commit changes in the `raney-org/mkdocs-materials` repository in VS Code, they will be committed as the configured bot and signed with the `GPG key`. This configuration will not affect other repositories on your system.

### How do you configure vs code to auto commit and push to a github remote?

Visual Studio Code does not have a built-in feature to auto-commit and push changes to a GitHub remote. However, you can create a simple script to automate the process and use the integrated terminal in VS Code to run the script whenever you want to commit and push your changes.

Here's a step-by-step guide:

1. Create a new file called `commit-and-push.sh` in the root of your repository.

2. Add the following content to the `commit-and-push.sh` file:

   ```bash
   #!/bin/bash
   # Change the commit message to your desired message
   commit_message="Auto-commit: Update files"

   # Add all changes to staging
   git add .

   # Commit the changes with the specified commit message
   git commit -m "$commit_message"

   # Push the changes to the remote repository
   git push
   ```

3. Save the file and close it.

4. Make the script executable by running the following command in the integrated terminal in VS Code:

   ```bash
   chmod +x commit-and-push.sh
   ```

5. Now, whenever you want to auto-commit and push your changes to the GitHub remote, simply run the script in the integrated terminal:

   ```bash
   ./commit-and-push.sh
   ```

This script will stage all changes, commit them with the specified commit message, and push the changes to the remote repository.

Please note that this method is manual and requires you to run the script each time you want to commit and push changes. There is no built-in feature in VS Code to automatically commit and push changes on a predefined schedule or event.

### What is a git sub module and what is a git tracking branch

A Git submodule and a Git tracking branch are two different concepts in Git. Let me explain each one:

1. Git Submodule:

A Git submodule is a mechanism for including an external Git repository within another Git repository. It allows you to keep another repository as a subdirectory within your main repository while maintaining its history. This is particularly useful when you want to include a library or a shared component in your project that is developed and maintained in a separate repository.

When you add a submodule to your repository, Git stores a reference to the submodule's commit, rather than storing the entire submodule's code. This keeps the main repository lightweight and allows you to update the submodule independently.

To add a submodule to your repository, use the following command:[^4]

[^4]:
    Replace `<repository_url>` with the URL of the external repository you want to include, and `<path_to_submodule>` with the desired path for the submodule within your main repository.

```bash
git submodule add <repository_url> <path_to_submodule>
```

2. Git Tracking Branch:

A Git tracking branch is a local branch that is connected to a remote branch. When you push or pull changes, the tracking branch automatically knows which remote branch to interact with. This makes it easier to stay in sync with the remote repository, as you don't have to specify the remote branch each time you push or pull changes.

By default, when you clone a remote repository or create a new branch from a remote branch, Git sets up a tracking relationship between the local and remote branches. You can also set up a tracking branch manually by using the following command:

```bash
git branch --track <local_branch> <remote_branch>
```

Replace `<local_branch>` with the name of the local branch you want to create, and `<remote_branch>` with the name of the remote branch you want to track (in the format `origin/branch_name`).

In summary, a Git submodule is a way to include an external repository within your main repository, while a Git tracking branch is a local branch that is connected to a remote branch for easier synchronization.

### can you give me an example of the file structure for using sub modules? say I have my main git repo at /home/raneydazed/pr/ and I have the sub module at /home/raneydazed/pr/sub-mod/. how would I refer to the sub module in the git submodule add command

In your example, if you have your main Git repository at `/home/raneydazed/pr/` and you want to add a submodule at `/home/raneydazed/pr/sub-mod/`, you should use a relative path for the submodule when running the `git submodule add command`.

First, navigate to your main repository:

```shell
cd /home/raneydazed/pr/
```

Now, assuming the submodule's remote repository URL is `https://github.com/user/submodule-repo.git`, you can add the submodule using the following command[^5]:

```bash
git submodule add https://github.com/user/submodule-repo.git sub-mod
```

This command will create a new directory called `sub-mod` within your main repository at `/home/raneydazed/pr/sub-mod/` and clone the submodule repository into it. The submodule's commit reference will be stored in the `.gitmodules` file in the root of your main repository.

The resulting file structure will look like this:

[^5]:
    Remember to replace `https://github.com/user/submodule-repo.git` with the actual remote repository URL of the `submodule` you want to add.

```shell
/home/raneydazed/pr/
│   .git/
│   .gitmodules
│   ...
└───sub-mod/
    │   .git/
    │   ...
```

or:

``` mermaid
graph TD
A[/home/raneydazed/pr/] -->|git submodule add ../sub-mod/| B[/home/raneydazed/pr/sub-mod/]
A/.git -->|git submodule add ../sub-mod/| B/.git
```

or:

``` mermaid
graph TD
A[/home/raneydazed/pr/] -->|contains| B[.git/]
A[/home/raneydazed/pr/] -->|contains| C[.gitmodules]
A[/home/raneydazed/pr/] -->|contains| D[...]
A[/home/raneydazed/pr/] -->|contains| E[sub-mod/]
E[sub-mod/] -->|contains| F[.git/]
E[sub-mod/] -->|contains| G[...]
```

## Can you expand on git tracking branches and how they are used, as compared to comitting to main/master

## Use cases and reasons for using tracking branches

**Collaboration:** Tracking branches are particularly useful when you collaborate with a team on a project. Each team member can create their own local tracking branches to work on different features or bug fixes. These tracking branches will be connected to remote branches, allowing team members to easily stay in sync with the remote repository and share their work.

**Isolation:** Tracking branches allow you to isolate your work from the main branch. This is helpful when you're working on a new feature or bug fix that might take some time to complete. By using a separate tracking branch, you can experiment and make changes without affecting the stability of the main branch.

## How tracking branches work compared to committing to the main branch

When you commit changes to the main branch, you're directly modifying the primary branch in your repository. This can be risky, especially if you're working on a large-scale project with multiple contributors. By committing directly to the main branch, your changes might conflict with others' work, or you might accidentally introduce bugs or unstable features.

On the other hand, when you use a tracking branch, you create a separate branch that is connected to a remote branch. You can commit your changes to this tracking branch without affecting the main branch. Once your work is complete and tested, you can merge your tracking branch into the main branch, ensuring that your changes are integrated smoothly and safely.

**Checking the tracking status:** To see the tracking status of your branches, you can use the following command:

```shell
git branch -vv
```

???+ note

    This command will display a list of your local branches along with their tracking relationships and the differences between the local and remote branches.

**Merging changes:** Once you've completed your work on a tracking branch and tested it, you can merge the changes back into the main branch. First, switch to the main branch:

```shell
   git checkout main
```

Then, merge your tracking branch into the main branch:[^6]

[^6]:
    Replace `<your_tracking_branch>` with the name of your tracking branch. This command will merge the changes from your tracking branch into the main branch, ensuring a smooth and safe integration.

```shell
   git merge <your_tracking_branch>
```

In summary, tracking branches provide a convenient way to collaborate, isolate your work, and synchronize changes with remote branches. They allow you to work on features or bug fixes independently without affecting the main branch and help maintain a stable and clean project history.

### Do you normally work directly on your tracking branch and not on main or master? is there any best practices surrounding tracking branches

Yes, it's a common and recommended practice to work directly on tracking branches (or any feature/bugfix branches) rather than working directly on the main or master branch. This approach is part of the best practices surrounding branch management in Git, which include:

1. Keep the main branch stable: The main or master branch should always be stable and production-ready. By working directly on tracking branches or feature branches, you ensure that any experimental or in-progress work does not affect the stability of the main branch.

2. Create branches for features or bug fixes: When working on a new feature or fixing a bug, create a separate branch (often a tracking branch) for that specific task. This allows you to isolate your work, making it easier to manage and review changes.

3. Use descriptive branch names: When creating a new branch, use a descriptive name that reflects the purpose of the branch (e.g., `feature/user-authentication` or `bugfix/payment-processing`). This makes it easier to understand the purpose of each branch and helps keep your repository organized.

4. Pull changes from the main branch regularly: While working on a tracking branch or feature branch, it's important to regularly pull changes from the main branch to keep your branch up-to-date. This helps prevent potential merge conflicts when you're ready to merge your changes back into the main branch.

   ```shell
   git checkout your_tracking_branch
   git pull origin main
   ```

5. Review and test changes before merging: Before merging your tracking branch or feature branch into the main branch, ensure that your changes have been thoroughly reviewed and tested. This helps maintain the stability and quality of the main branch.

6. Merge or rebase: When you're ready to merge your changes back into the main branch, you can use the git merge command or, alternatively, use git rebase to keep a linear commit history. Rebasing can make the commit history cleaner and easier to understand, but it requires more care and attention, as it rewrites the commit history.

    ```s
    # Merging
    git checkout main
    git merge your_tracking_branch

    # Rebasing
    git checkout your_tracking_branch
    git rebase main
    git checkout main
    git merge your_tracking_branch
    ```

7. Delete branches after merging: Once you've successfully merged a tracking branch or feature branch into the main branch, delete the branch to keep your repository clean and organized.

    ```shell
    git branch -d your_tracking_branch
    ```

By following these best practices, you can maintain an organized, stable, and clean Git repository while collaborating with your team on various tasks.

### how do I use the cache action to cache this

I asked it how to more or less use the cache action in github to speed up actions. Here is an (collapsed) example of `ci.yml` in the root directory of my GH repo, the full path is `.github/workflows/ci.yml`

```shell
name: ci 
on:
  push:
    branches:
      - master 
      - main
  pull_request:
  workflow_dispatch:
permissions:
  contents: write

concurrency:
  group: ${{ github.ref }}
  cancel-in-progress: true

jobs:
  add-contributors:
    runs-on: ubuntu-latest
    if: github.ref == 'refs/heads/main'
    steps:

    - name: Checkout Contributors
      uses: actions/checkout@v3

    - name: Add Contributors
      uses: BobAnkh/add-contributors@master
      with:
        REPO_NAME: 'Raney-org/mkdocs-material'
        CONTRIBUTOR: '### Contributors'
        COLUMN_PER_ROW: '6'
        ACCESS_TOKEN: ${{ secrets.PAC_TOKEN }}
        IMG_WIDTH: '100'
        FONT_SIZE: '14'
        PATH: '/README.md'
        COMMIT_MESSAGE: 'docs(README): update contributors'
        AVATAR_SHAPE: 'round'

  build:
    runs-on: ubuntu-latest
    if: github.event.repository.fork == false && github.event_name != 'pull_request'
    outputs:
      url: ${{ steps.cloudflare.outputs.url }}
    steps:
      - name: Checkout
        uses: actions/checkout@v3

      - name: Setup Python 3
        uses: actions/setup-python@v4
        with:
          python-version: 3.x

      - name: Upgrade PIP
        run: pip install --upgrade pip

      - name: Install wheel
        run: pip install wheel

      - name: Install Cairosvg
        run: pip install pillow cairosvg

      - name: Install Table Reader Plugin
        run: pip install mkdocs-table-reader-plugin

      - name: Install openpyxl
        run: pip install openpyxl

      - name: Install glightbox??
        run: pip install mkdocs-glightbox

      - name: Cache
        uses: actions/cache@v2
        with:
          key: ${{ github.ref }}
          path: .cache

      - name: Install Mkdocs Material
        run: pip install mkdocs-material

      - name: Build mkdocs
        run: mkdocs build

      - name: Publish to Cloudflare Pages
        id: cloudflare
        uses: cloudflare/pages-action@1
        with:
          apiToken: ${{ secrets.CLOUDFLARE_API_TOKEN }}
          accountId: ${{ secrets.CLOUDFLARE_ACCOUNT_ID }}
          projectName: mkdocs-material
          directory: site
          gitHubToken: ${{ secrets.PAC_TOKEN }}

  webhook:
    name: 'webhook'
    runs-on: self-hosted
    needs: [build]
    if: always() && github.event_name != 'pull_request'
    steps:
      - name: Workflow-Conclusion Actions
        uses: technote-space/workflow-conclusion-action@v3

      - name: Send Discord Notification
        uses: sarisia/actions-status-discord@v1
        with:
          webhook: ${{ secrets.DISCORD_WEBHOOK }}
          description: "URL: ${{ needs.build.outputs.url }}"
          status: ${{ env.WORKFLOW_CONCLUSION }}
```

To cache the dependencies for your GitHub Actions workflow, you can use the `actions/cache@v2` action. In your case, you can cache the Python packages installed with `pip`. Here's an updated version of your workflow that caches the Python packages:

```shell
build:
  runs-on: ubuntu-latest
  if: github.event.repository.fork == false && github.event_name != 'pull_request'
  outputs:
    url: ${{ steps.cloudflare.outputs.url }}
  steps:
    - name: Checkout
      uses: actions/checkout@v3

    - name: Setup Python 3
      uses: actions/setup-python@v4
      with:
        python-version: 3.x

    - name: Upgrade PIP
      run: pip install --upgrade pip

    - name: Cache Python packages
      uses: actions/cache@v2
      with:
        path: ~/.cache/pip
        key: ${{ runner.os }}-pip-${{ hashFiles('**/requirements.txt', '**/setup.py') }}
        restore-keys: |
          ${{ runner.os }}-pip-

    - name: Install wheel
      run: pip install wheel

    - name: Install Cairosvg
      run: pip install pillow cairosvg

    - name: Install Table Reader Plugin
      run: pip install mkdocs-table-reader-plugin

    - name: Install openpyxl
      run: pip install openpyxl

    - name: Install glightbox??
      run: pip install mkdocs-glightbox

    - name: Install Mkdocs Material
      run: pip install mkdocs-material

    - name: Build mkdocs
      run: mkdocs build
```

!!! note

    I kept the cache action out of my submission to the bot.

This workflow now includes a "Cache Python packages" step that uses `actions/cache@v2` to cache the Python packages installed with `pip`. The cache key is based on the hash of any `requirements.txt` and `setup.py` files in your repository. If these files change, the cache will be invalidated, and new packages will be installed and cached.

Please note that if you don't have a `requirements.txt` or `setup.py` file in your repository, you can create a `requirements.txt` file and list all the packages you want to install:

```bash
wheel
pillow
cairosvg
mkdocs-table-reader-plugin
openpyxl
mkdocs-glightbox
mkdocs-material
```

Then, you can simplify the installation steps in your workflow by using:

```shell
    - name: Install Python packages
      run: pip install -r requirements.txt
```

Here's the updated version of your workflow using the requirements.txt file:

```shell
build:
  runs-on: ubuntu-latest
  if: github.event.repository.fork == false && github.event_name != 'pull_request'
  outputs:
    url: ${{ steps.cloudflare.outputs.url }}
  steps:
    - name: Checkout
      uses: actions/checkout@v3

    - name: Setup Python 3
      uses: actions/setup-python@v4
      with:
        python-version: 3.x

    - name: Upgrade PIP
      run: pip install --upgrade pip

    - name: Cache Python packages
      uses: actions/cache@v2
      with:
        path: ~/.cache/pip
        key: ${{ runner.os }}-pip-${{ hashFiles('**/requirements.txt') }}
        restore-keys: |
          ${{ runner.os }}-pip-

    - name: Install Python packages
      run: pip install -r requirements.txt

    - name: Build mkdocs
      run: mkdocs build
```

This workflow now uses the `requirements.txt` file to install all Python packages in a single step, making the workflow cleaner and easier to maintain. The cache action will also use the `requirements.txt` file to determine when to invalidate the cache.

### is there a way to use the cache action with the pip install commands instead of using a requirements.txt file

Yes, you can use the cache action with the `pip install` commands without using a `requirements.txt` file. You can create a cache key based on the content of the workflow file itself or use a custom cache key. Here's an example of how to modify your workflow to cache Python packages without a `requirements.txt` file:

```shell
build:
  runs-on: ubuntu-latest
  if: github.event.repository.fork == false && github.event_name != 'pull_request'
  outputs:
    url: ${{ steps.cloudflare.outputs.url }}
  steps:
    - name: Checkout
      uses: actions/checkout@v3

    - name: Setup Python 3
      uses: actions/setup-python@v4
      with:
        python-version: 3.x

    - name: Upgrade PIP
      run: pip install --upgrade pip

    - name: Cache Python packages
      uses: actions/cache@v2
      with:
        path: ~/.cache/pip
        key: ${{ runner.os }}-pip-${{ hashFiles('.github/workflows/your-workflow-file.yml') }}
        restore-keys: |
          ${{ runner.os }}-pip-

    - name: Install wheel
      run: pip install wheel

    - name: Install Cairosvg
      run: pip install pillow cairosvg

    - name: Install Table Reader Plugin
      run: pip install mkdocs-table-reader-plugin

    - name: Install openpyxl
      run: pip install openpyxl

    - name: Install glightbox??
      run: pip install mkdocs-glightbox

    - name: Install Mkdocs Material
      run: pip install mkdocs-material

    - name: Build mkdocs
      run: mkdocs build
```

In this example, I've changed the cache key to be based on the content of the workflow file itself: `#!shell ${{ hashFiles('.github/workflows/your-workflow-file.yml') }}`. Replace `your-workflow-file.yml` with the actual name of your workflow file. This way, the cache will be invalidated if the workflow file changes, which might include changes to the package installation commands.

Please note that this approach is less precise than using a `requirements.txt` file, as any change to the workflow file will invalidate the cache, even if the installed packages remain the same. However, it still allows you to cache Python packages without using a `requirements.txt` file.

### Can you add conditionals with cache hit and cache miss

Certainly! You can use the `cache-hit` output of the `actions/cache` step to add conditional steps based on whether the cache was hit or missed. Here's an example of how to modify your workflow to include conditionals for cache hit and cache miss:

```shell
build:
  runs-on: ubuntu-latest
  if: github.event.repository.fork == false && github.event_name != 'pull_request'
  outputs:
    url: ${{ steps.cloudflare.outputs.url }}
  steps:
    - name: Checkout
      uses: actions/checkout@v3

    - name: Setup Python 3
      uses: actions/setup-python@v4
      with:
        python-version: 3.x

    - name: Upgrade PIP
      run: pip install --upgrade pip

    - name: Cache Python packages
      id: cache-pip
      uses: actions/cache@v2
      with:
        path: ~/.cache/pip
        key: ${{ runner.os }}-pip-${{ hashFiles('.github/workflows/your-workflow-file.yml') }}
        restore-keys: |
          ${{ runner.os }}-pip-

    - name: Install packages on cache miss
      if: steps.cache-pip.outputs.cache-hit != 'true'
      run: |
        pip install wheel
        pip install pillow cairosvg
        pip install mkdocs-table-reader-plugin
        pip install openpyxl
        pip install mkdocs-glightbox
        pip install mkdocs-material

    - name: Build mkdocs
      run: mkdocs build
```

In this example, I've added an `id` to the "Cache Python packages" step, which is `cache-pip`. Then, I've combined all the package installation commands into a single step called "Install packages on cache miss" and added a conditional `if` statement:

```shell
if: steps.cache-pip.outputs.cache-hit != 'true'
```

This step will only run if the cache is missed, meaning the packages will not be installed if the cache is hit. Replace `your-workflow-file.yml` with the actual name of your workflow file.

This approach allows you to conditionally execute steps based on the cache hit or cache miss status, reducing unnecessary package installations when the cache is hit.

### What is git squash

Git squash is a technique used to combine multiple commits into a single commit, which helps create a cleaner and more linear commit history. Squashing is often used when you have a series of small commits that represent incremental changes or work-in-progress updates, and you want to merge them into a single, meaningful commit before merging into another branch or pushing to a remote repository.

Git squash is typically performed using an interactive rebase. Here's a step-by-step guide on how to squash commits:

1. Make sure you're on the correct branch that contains the commits you want to squash. If not, switch to that branch:

    ```shell
    git checkout your-feature-branch
    ```

2. Start an interactive rebase for the last `n` commits, where `n` is the number of commits you want to squash:

    ```shell
    git rebase -i HEAD~n
    ```

    Replace `n` with the actual number of commits you want to squash.

3. Your default text editor will open with a list of the last `n` commits, each prefixed with the word `pick`. To squash a commit, change the word `pick` to `squash` or `s` for that commit. Leave the first commit in the list with `pick`.

    ```shell
    pick a1b2c3d First commit message
    squash e4f5g6h Second commit message
    squash i7j8k9l Third commit message
    ```

    Save and close the editor.

4. Git will now combine the selected commits into one. A new editor window will open, allowing you to edit the commit message for the combined commit. Update the commit message as needed, save, and close the editor.

5. Git will perform the squash, and your commit history will now have the selected commits combined into a single commit with the updated commit message.

Please note that squashing commits rewrites the commit history. Be cautious when using squash on commits that have already been pushed to a remote repository, as it may cause conflicts or issues for other collaborators. It's generally safe to squash commits that have not been pushed or shared with others.

[^3]:
    Replace `"Your Bot Name"` and `"your-bot-email@example.com"` with the actual bot name and email address.
    ```bash
    git config user.name "Your Bot Name"
    git config user.email "your-bot-email@example.com"
    ```



  [^1]: Note: this requires you to have `git` installed on your device.

  []: https://discord.com/channels/636941159704559617/636967268579803156/1099805846768193536