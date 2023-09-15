# Git: A Version Control System

In this project we will begin by explaining some background on version control tools, then move on to how to get Git running on your system and finally how to get it set up to start working with. At the end of this project you should understand why Git is around, why you should use it and you should be all set up to do so.

🔧 **Pre-requisites:**

- You must have some familiarity with Linux Commands
- Have GitBash installed on your system if you're using windows
- Must have created a GitHub/GitLab Account.
- If you're running Linux you can install git using the following options:

```bash
sudo apt install -y git # Ubuntu/Debian Linux

sudo yum install -y git # CentOS/Amazon Linux/RedHat

sudo dnf install -y git # Fedora
```
## About Version Control

What is “version control”, and why should you care? Version control is a system that records changes to a file or set of files over time so that you can recall specific versions later. If you are a graphic or web designer and want to keep every version of an image or layout (which you would most certainly want to), a Version Control System (VCS) is a very wise thing to use. 

It allows you to revert selected files back to a previous state, revert the entire project back to a previous state, compare changes over time, see who last modified something that might be causing a problem, who introduced an issue and when, and more. Using a VCS also generally means that if you screw things up or lose files, you can easily recover. In addition, you get all this for very little overhead.

## Key Concepts

### 1. Repository (Repo)

A Git repository is a collection of files and their entire history of changes. It can be local (on your computer) or remote (hosted on a server). Repositories are the core of Git and contain all the project's files and their change history.

### 2. Commit

A commit is a snapshot of the repository at a specific point in time. Each commit records changes to files, along with a unique identifier (hash), a commit message describing the changes, and a pointer to the previous commit, forming a commit history.

### 3. Branch

A branch is a separate line of development within a repository. It allows multiple contributors to work on different features or fixes simultaneously without interfering with each other. The default branch is usually called `master` or `main`.

### 4. Clone

Cloning a repository creates a local copy of a remote repository, allowing you to work on the project locally. This is the primary way to start contributing to a Git project.

## Certainly! Here are the commands used at each of the three Git states:

## The Three States

Pay attention now—here is the main thing to remember about Git if you want the rest of your learning process to go smoothly. Git has three main states that your files can reside in:

1. **Modified** 📝: This means that you have changed the file but have not committed it to your database yet.
   
   Commands:
   - Modify a file.
   - Check the status: `git status`.

2. **Staged** 🚧: This means that you have marked a modified file in its current version to go into your next commit snapshot.
   
   Commands:
   - Stage changes: `git add <file>`.
   - Check the status: `git status`.

3. **Committed** ✅: This means that the data is safely stored in your local database.
   
   Commands:
   - Commit changes: `git commit -m "Commit message"`.
   - Check commit history: `git log`.

This leads us to the three main sections of a Git project:

- **Working Tree** 🌳: The area where you modify files.
- **Staging Area** 📦: Where you stage changes before committing.
- **Git Directory** 🗄️: The local database where committed changes are stored.

![git workflow](./images/git-project-2.png)

📝 Remembering these states and commands is crucial for understanding Git's workflow and version control process.

## Basic Git Workflow

1. **Initialization**: Create a new Git repository or clone an existing one.
   ```bash
   git init  # Initialize a new repository
   git clone <repository-url>  # Clone an existing repository
   ```

2. **Add and Commit**: Stage changes and commit them to the repository.
   ```bash
   git add <file>  # Stage a file for commit
   git commit -m "Commit message"  # Commit staged changes
   ```

3. **Branching and Merging**:
   - Create a new branch: `git branch <branch-name>`
   - Switch to a branch: `git checkout <branch-name>`
   - Merge changes from one branch into another: `git merge <source-branch>`

4. **Remote Repositories**:
   - Add a remote: `git remote add <name> <repository-url>`
   - Pull changes from a remote: `git pull <remote> <branch>`
   - Push changes to a remote: `git push <remote> <branch>`

5. **History and Logs**:
   - View commit history: `git log`
   - View differences between commits: `git diff <commit1> <commit2>`

**💡 Side Hustle Task 1 ⏱️:** 

### Task: Create and Initialize a Folder

Create a Folder on your local system and do the following:
- Create a folder with the name `project-1`
- Open the folder with Gitbash/Terminal/iterm and run `git init`
- Create a file `gitfile-1.txt` and run `git status`
- Create and switch to a new branch using `git checkout -b <branch_name>`

## First-Time Git Setup

Now that you have Git on your system, you'll want to do a few things to customize your Git environment. This setup process should be done only once on any given computer, and the configurations will persist between upgrades. You can also modify these settings at any time by running the appropriate commands.

Git provides a tool called `git config` that allows you to manage configuration variables controlling various aspects of Git's behavior. These variables can be stored in three different places:

1. System-level configuration: Applies to all users on the system.
2. User-level configuration: Applies to your specific user account.
3. Repository-level configuration: Applies only to a particular Git repository.

### Setting Your Identity

The first thing you should do after installing Git is to set your identity. This information will be associated with your commits.

```bash
   git config --global user.name "John Doe"
   git config --global user.email johndoe@example.com
```

NB: Replace `"Your Name"` with your actual name and `"youremail@example.com"` with your email address consistent with your GitHub/GitLab account profile.

### Configuring Editor

You can specify your preferred text editor for Git messages and other interactions.

```bash
git config --global core.editor "your-editor-of-choice"
```

Replace `"your-editor-of-choice"` with the command to launch your preferred text editor (e.g., `"nano"`, `"vim"`, `"code"`).

### Checking Your Configuration

To confirm your Git configuration settings, you can use:

```bash
git config --list
```
This command will display all the configuration variables and their values; 

## **`output`**

```bash
user.name=John Doe
user.email=johndoe@example.com
```
## Getting Help

If you ever need help while using Git, there are three equivalent ways to get the comprehensive manual page (manpage) help for any of the Git commands:
```bash
$ git help <verb>
$ git <verb> --help
$ man git-<verb>
```
For example, you can get the manpage help for the `git config` command by running this:
```bash
$ git help config
```
In addition, if you don’t need the full-blown manpage help, but just need a quick refresher on the available options for a Git command, you can ask for the more concise “help” output with the -h option, as in:

```bash
git add -h
```
## **`output`**
```bash
usage: git add [<options>] [--] <pathspec>...

    -n, --dry-run               dry run
    -v, --verbose               be verbose
    -i, --interactive           interactive picking
    -p, --patch                 select hunks interactively
    -e, --edit                  edit current diff and apply
    -f, --force                 allow adding otherwise ignored files
    -u, --update                update tracked files
```
## Getting a Git Repository

You typically obtain a Git repository in one of two ways:

- You can take a local directory that is currently not under version control, and turn it into a Git repository, or

- You can clone an existing Git repository from elsewhere.

In either case, you end up with a Git repository on your local machine, ready for work.

### Initializing a Repository in an Existing Directory

If you have a project directory that is currently not under version control and you want to start controlling it with Git, you first need to go to that project’s directory. If you’ve never done this, it looks a little different depending on which system you’re running:

***for Linux:***
```bash 
$ cd /home/user/my_project
```

***for macOS:***

```bash 
$ cd /Users/user/my_project
```

***for Windows:***

```bash
$ cd C:/Users/user/my_project
```
**and type:**

```bash
$ git init
```
This creates a new subdirectory named ``.git`` that contains all of your necessary repository files — a Git repository skeleton.

### Cloning an Existing Repository

If you want to get a copy of an existing Git repository — for example, a project you’d like to contribute to — the command you need is ``git clone``

You clone a repository with ``git clone <url>``. For example, if you want to clone a dareyio assignment repo called Linux_Project, you can do so like this:

```bash
git clone https://github.com/dareyio/Linux_Project
```

That creates a directory named ``Linux_Project`` on your local machine, initializes a ``.git`` directory inside it, pulls down all the data for that repository, and checks out a working copy of the latest version. If you go into the new ``Linux_Project`` directory that was just created, you’ll see the project files in there, ready to be worked on or used.

If you want to clone the repository into a directory named something other than ``Linux_Project``, you can specify the new directory name as an additional argument:

```bash
git clone https://github.com/dareyio/Linux_Project mylinux_project
```

The above 👆 command does the same thing as the previous one, but the target directory is called ``mylinux_project``

**🤔 Side Hustle Task 2 ⌛️:** 

### Git Task: Create, Commit, and Clone

### Objective

Practice the basic Git workflow by creating a Git repository, committing changes, and cloning the repository to your local machine.

### Task Steps

1. **Create a Git Repository**

   - Open your terminal or Git Bash.
   - Navigate to the directory where you want to create your Git repository.
   - Run the following command to initialize a new Git repository:

     ```shell
     git init my-first-repo
     ```

2. **Add a File and Commit Changes**

   - Inside the "my-first-repo" directory, create a new text file, e.g., "hello.txt."
   - Add some text to the "hello.txt" file.
   - Run the following commands to commit your changes:

     ```shell
     git add hello.txt
     git commit -m "Add a greeting message"
     ```

3. **Create a Remote Repository (Optional)**

   - If you want to practice with a remote repository (e.g., on GitHub or GitLab), create one now and note the repository URL.

4. **Clone the Repository**

   - Navigate to the directory where you want to clone the repository (outside of "my-first-repo").
   - Run the following command to clone the repository:

     ```shell
     git clone <repository-url> my-cloned-repo
     ```
   - Replace `<repository-url>` with the URL of the remote repository you created.
   - This will create a local copy of the repository named "my-cloned-repo."

## Git Branching

Git branching is a fundamental concept in Git that allows developers to work on different features or fixes in parallel without interfering with each other. Branches provide isolation and a structured way to manage code changes in a Git repository.

### Key Concepts

### 1. **Master Branch**

- The `master` branch is the default and primary branch in a Git repository.
- It typically represents the stable and production-ready version of the code.
- Avoid making direct changes to the `master` branch to maintain code stability.

### 2. **Creating a Branch**

- To create a new branch, use the following command:

  ```shell
  git branch <branch-name>
  ```

- To switch to the new branch, use:

  ```shell
  git checkout <branch-name>
  ```

- Alternatively, you can create and switch to a new branch in one step:

  ```shell
  git checkout -b <branch-name>
  ```

### 3. **Working on a Branch**

- When you're on a branch, any changes you make are isolated to that branch.
- You can commit your changes on the branch as you work on new features or bug fixes.

### 4. **Merging Branches**

- Merging combines changes from one branch (the source) into another (the target).
- To merge a branch into `master`, for example, you would do the following:

  ```shell
  git checkout master # Switching back to the master branch
  git merge <source-branch>
  ```

### 5. **Branch Visualization**

- You can visualize the branching structure of a repository using tools like `git log` with options or specialized graphical Git tools.

## Common Branching Workflows

### 1. **Feature Branch Workflow**

- Create a new branch for each new feature or enhancement.
- Develop and test the feature on the feature branch.
- Merge the feature branch into `master` when it's complete.

### 2. **Git Flow Workflow**

- A more structured branching model with specific branches for features, releases, and hotfixes.
- Uses branches like `feature/`, `release/`, `hotfix/`, and `develop`.

For more details and advanced branching strategies, refer to the [official Git documentation](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging).

## Generating Your SSH Public Key

Many Git servers authenticate using SSH public keys. In order to provide a public key, each user in your system must generate one if they don’t already have one. This process is similar across all operating systems. First, you should check to make sure you don’t already have a key. By default, a user’s SSH keys are stored in that user’s ``~/.ssh `` directory. You can easily check to see if you have a key already by going to that directory and listing the contents:

```
cd ~/.ssh
ls
authorized_keys2  id_dsa       known_hosts
config            id_dsa.pub
```

If you don’t have these files (or you don’t even have a ``.ssh`` directory), you can create them by running a program called ``ssh-keygen``, which is provided with the SSH package on Linux/macOS systems and comes with Git for Windows:

```
ssh-keygen -t ed25519 -C "your_email@example.com"
```

- *Note: If you are using a legacy system that doesn't support the Ed25519 algorithm, use:*
```
 ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

## **`output`**
```bash
Generating public/private rsa key pair.
Enter file in which to save the key (/home/schacon/.ssh/id_rsa):
Created directory '/home/schacon/.ssh'.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/schacon/.ssh/id_rsa.
Your public key has been saved in /home/schacon/.ssh/id_rsa.pub
```
For more details on how to generate ssh keys, refer to the [GitHub Authentication Documentation Page.](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent).

