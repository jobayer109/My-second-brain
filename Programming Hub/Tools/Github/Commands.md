# 🔸 init

-  **Creates a New Repository**: It initializes a new Git repository in the current directory. This means Git will start tracking changes to the files in this directory.

-  **Creates a `.git` Directory**: It sets up a `.git` directory in your project folder. This directory contains all the metadata and version history for your Git repository, including configuration files, hooks, and information about the commits.

-  **Prepares for Version Control**: After running `git init`, you can start tracking files, making commits, and using other Git commands to manage the version history of your project.

```bash
cd /path/to/your/project
git init
```

---

# 🔸add

 **Purpose**: The `git add` command is used to stage changes (modifications, new files, deletions) before committing them to the Git repository. This tells Git that you want to include the changes in the next commit.
  
### Common Usage:
1. **Stage a single file**:
   ```bash
   git add index.js
   ```

2. **Stage multiple specific files**:
   ```bash
   git add file1 file2
   ```

3. **Stage all changes in the working directory**:
   ```bash
   git add .
   ```
   This stages all modified and new files recursively from the current directory.

4. **Stage specific changes within a file (interactive mode)**:
   ```bash
   git add -p
   ```
   Allows you to selectively stage parts of a file, such as specific changes or hunks.

### Notes:
- **Staging area**: `git add` moves changes to the staging area, preparing them for a commit.
- **Undo staging**: If you accidentally stage a file, you can remove it from the staging area with:
   ```bash
   git reset <file-name>
   ```

---

# 🔸commit
**git commit** is used to save changes to the local repository. It captures a snapshot of the project's current state. 

### Key Points:
- **Staging Area**: Files must be added to the staging area using `git add` before committing.
- **Best Practices for Commit Messages**:
  - Use **imperative** mood (e.g., "Add login page" not "Added login page").
  - Keep the message **short** (50 chars or less for the summary).
  - Optionally, follow with a longer explanation after a blank line.
  
### Common Options:
- `-m`: Add a commit message inline (e.g., `git commit -m "message"`)
- `--amend`: Edit the last commit (useful for fixing mistakes)
- `--no-edit`: Amend without changing the commit message.

### Commit Types:
- **feat**: New feature
- **fix**: Bug fix
- **refactor**: Code restructuring without changing functionality
- **docs**: Documentation changes

### Example Workflow:
```bash
git add .
git commit -m "fix: resolve login issue"
```

---

# 🔸push

**git push** is used to upload local repository changes to a remote repository (e.g., GitHub, GitLab).

### Key Points:
- **Sends Commits**: Transfers your local commits to a remote branch.
- **Common Syntax**: 
  ```bash
  git push <remote> <branch>
  ```
  - Example: `git push origin main`

### Push Process:
1. **Commit Changes**: Ensure you have committed changes locally (`git commit`).
2. **Push to Remote**: Upload changes with `git push`.

### Common Options:
- `git push`: Push changes from the current branch to the associated remote branch.
- `-u`: Set the upstream branch for future `git push` without specifying the remote and branch.
  - Example: `git push -u origin main`
- `--force` or `-f`: Force push to overwrite remote history (use with caution).

### Example Workflow:
```bash
git add .
git commit -m "feat: add search functionality"
git push origin main
```

---

# 🔸pull

**`git pull`** = `git fetch` + `git merge`

1. **Purpose**:  
   The `git pull` command updates your local repository by fetching and merging changes from a remote repository into your current branch.

2. **Basic Syntax**:
   ```bash
   git pull <remote> <branch>
   ```
   - `remote`: The name of the remote repository (default is `origin`).
   - `branch`: The name of the branch you want to pull from (e.g., `main` or `master`).

3. **Example**:
   ```bash
   git pull origin main
   ```
   This command fetches changes from the `main` branch on the `origin` remote and merges them into the current branch.

4. **Fast-forward Merge**:
   If there are no conflicts, Git performs a fast-forward merge, updating your branch without creating a new commit.

5. **Handling Merge Conflicts**:
   If your local changes conflict with the remote, Git will pause and allow you to resolve the conflicts manually before completing the merge.

6. **Common Options**:
   - `--rebase`: Rebase your changes on top of the fetched branch, avoiding a merge commit.
     ```bash
     git pull --rebase
     ```

---

# 🔸status

**`git status`**: Check the current state of your working directory and staging area.

1. **Purpose**:  
   The `git status` command provides information on:
   - Untracked files
   - Changes not yet staged
   - Changes staged for the next commit
   - Files that have been modified

2. **Basic Syntax**:
   ```bash
   git status
   ```

3. **Key Sections**:
   - **Untracked files**: Files not yet added to version control.
   - **Changes not staged for commit**: Modified files, but changes not yet added (`git add` required).
   - **Changes to be committed**: Files staged and ready to be committed.

4. **Example Output**:
   ```bash
   On branch main
   Your branch is up to date with 'origin/main'.
   
   Changes not staged for commit:
     (use "git add <file>..." to update what will be committed)
     (use "git restore <file>..." to discard changes in working directory)
           modified:   file1.txt
           modified:   file2.js
   
   Untracked files:
     (use "git add <file>..." to include in what will be committed)
           newfile.py
   ```

5. **Usefulness**:
   - Helps track changes before committing.
   - Detects untracked, modified, or staged files.

---

# 🔸diff

**`git diff`**: Shows changes between commits, branches, or the working directory.

1. **Purpose**:  
   The `git diff` command is used to compare differences between:
   - Working directory and the staging area
   - Staging area and the last commit
   - Two commits or branches

2. **Basic Syntax**:
   ```bash
   git diff [options] [<path>]
   ```

3. **Common Use Cases**:
   - **Show unstaged changes**:
     ```bash
     git diff
     ```
     Compares the working directory with the staging area, displaying changes not yet staged.

   - **Show staged changes**:
     ```bash
     git diff --staged
     ```
     Compares staged changes (those added via `git add`) with the last commit.

   - **Compare specific branches or commits**:
     ```bash
     git diff <branch1> <branch2>
     ```
     Shows differences between two branches or commits.

---

# 🔸log

- **Basic Log**:  
  `git log`  
  Displays the commit history, showing author, date, and commit message.

- **One-line Log**:  
  `git log --oneline`  
  Shows a brief version with just commit hashes and messages.

- **Limit Number of Commits**:  
  `git log -n <number>`  
  E.g., `git log -n 5` shows the last 5 commits.

- **Graph View**:  
  `git log --graph --oneline --decorate --all`  
  Visualizes the commit history with branches and merges.

- **Show Commits by Author**:  
  `git log --author="<author name>"`  
  Filters commits by the specified author.

- **Date Range**:  
  `git log --since="YYYY-MM-DD" --until="YYYY-MM-DD"`  
  Displays commits within a date range.

- **File History**:  
  `git log <file>`  
  Shows the commit history of a specific file.

- **Show Diff with Commit**:  
  `git log -p`  
  Shows the changes introduced in each commit (includes diffs).
  
---

# 🔸show
- **Basic Usage**:  
  `git show <commit>`  
  Displays details about a specific commit, including the diff of changes, author, and date.

- **Show a File in a Commit**:  
  `git show <commit>:<file_path>`  
  Displays the content of a file at a specific commit.

- **Show Changes for a Branch or Tag**:  
  `git show <branch_name>` or `git show <tag_name>`  
  Shows the changes introduced by the most recent commit on the branch or tag.

- **Limit Diff Context**:  
  `git show --stat`  
  Provides a summary of changes, including file names, insertions, and deletions.

- **Only Commit Message and Metadata**:  
  `git show --no-patch`  
  Displays the commit message, author, and date without showing the changes (diff).

- **Show Changes of Specific File in Commit**:  
  `git show <commit> -- <file_path>`  
  Shows only the changes for the specified file in the given commit.

---

# 🔸reset
The `git reset` command is used to undo changes by moving the current branch pointer to a previous commit. It can adjust the staging area and working directory based on the options:

1. **`git reset --soft [commit]`**: Moves the HEAD to the specified commit but keeps changes staged (in the index).
   ```bash
   git reset --soft 123abc
   ```
   *Example:* If you want to undo the last commit but keep the changes staged for a new commit.

2. **`git reset --mixed [commit]` (default)**: Moves the HEAD to the specified commit, un-stages the changes (removes them from the index) but keeps them in the working directory.
   ```bash
   git reset --mixed 123abc
   ```
   *Example:* If you want to undo a commit and prepare changes to be staged again for another commit.

3. **`git reset --hard [commit]`**: Moves the HEAD to the specified commit and discards all changes in the staging area and working directory.
   ```bash
   git reset --hard 123abc
   ```
   *Example:* If you want to undo a commit and completely discard all changes from that point.

---

# 🔸branch
The `git branch` command is used to manage branches in a Git repository. It allows you to create, list, rename, and delete branches.

1. **List all branches**: 
   ```bash
   git branch
   ```
   *Example:* Shows all local branches. The current branch is marked with an asterisk (`*`).

2. **Create a new branch**: 
   ```bash
   git branch new-feature
   ```
   *Example:* Creates a new branch called `new-feature` from the current HEAD.

3. **Switch to another branch** (with `git checkout` or `git switch`):
   ```bash
   git checkout new-feature
   ```
   *Example:* Switches to the `new-feature` branch.

   Or using `git switch`:
   ```bash
   git switch new-feature
   ```

4. **Delete a branch**:
   ```bash
   git branch -d old-feature
   ```
   *Example:* Deletes the branch `old-feature` if it has been fully merged.

5. **Rename a branch**:
   ```bash
   git branch -m new-name
   ```
   *Example:* Renames the current branch to `new-name`.

6. **List all remote and local branches**:
   ```bash
   git branch -a
   ```
   *Example:* Displays all branches, including those on the remote.

---

# 🔸checkout
The `git checkout` command is used to switch branches, restore files, or even create new branches in a Git repository. It's versatile for both navigating and managing project states.

1. **Switch to an existing branch**:
   ```bash
   git checkout branch-name
   ```
   *Example:* Switches to the `branch-name` branch.

2. **Create and switch to a new branch**:
   ```bash
   git checkout -b new-feature
   ```
   *Example:* Creates a new branch called `new-feature` and switches to it.

3. **Restore a specific file to the last committed state**:
   ```bash
   git checkout HEAD -- file.txt
   ```
   *Example:* Restores `file.txt` to its state in the last commit (removes uncommitted changes).

4. **Checkout a specific commit** (detached HEAD state):
   ```bash
   git checkout 123abc
   ```
   *Example:* Switches to a specific commit by its hash `123abc`, allowing you to explore or work in a previous commit state.

⚠️ Note: `git switch` and `git restore` were introduced to replace some functions of `git checkout` for clarity, but `checkout` remains widely used.

---


# 🔸merge
The `git merge` command is used to combine changes from different branches in a Git repository. It integrates the history of two branches, allowing you to bring together work done in parallel.

1. **Basic merge**:
   ```bash
   git checkout main
   git merge feature-branch
   ```
   *Example:* Switches to the `main` branch and merges changes from the `feature-branch` into `main`. This incorporates all commits from `feature-branch` into `main`.

2. **Fast-forward merge**:
   If `main` has not diverged from `feature-branch`, a fast-forward merge occurs automatically.
   ```bash
   git merge feature-branch
   ```
   *Example:* If `main` was created before `feature-branch`, merging will move the `main` pointer forward to `feature-branch`.

3. **Creating a merge commit**:
   If both branches have diverged, a merge commit will be created.
   ```bash
   git checkout main
   git merge feature-branch
   ```
   *Example:* If there are changes in both `main` and `feature-branch`, Git will create a new commit that combines the changes, allowing you to keep both histories.

4. **Merge with conflict resolution**:
   If there are conflicting changes between branches, Git will pause the merge process and prompt you to resolve conflicts.
   ```bash
   git merge feature-branch
   ```
   *Example:* If changes in `main` and `feature-branch` affect the same line in a file, you must manually resolve the conflicts, mark them as resolved, and then commit the merge:
   ```bash
   git add resolved-file.txt
   git commit
```


---

# 🔸stash
The `git stash` command is used to temporarily save changes in your working directory that you aren't ready to commit yet. This allows you to switch branches or perform other tasks without losing your current progress.

1. **Stash changes**:
   ```bash
   git stash
   ```
   *Example:* Saves all uncommitted changes (both staged and unstaged) to a new stash entry, reverting your working directory to the last commit.

2. **Stash with a message**:
   ```bash
   git stash save "descriptive message"
   ```
   *Example:* Stashes changes with a specific message for easier identification later.

3. **List stashed changes**:
   ```bash
   git stash list
   ```
   *Example:* Displays a list of all stashed entries, including their names (like `stash@{0}`, `stash@{1}`, etc.).

4. **Apply the most recent stash**:
   ```bash
   git stash apply
   ```
   *Example:* Restores the changes from the most recent stash entry without removing it from the stash list.

5. **Apply a specific stash**:
   ```bash
   git stash apply stash@{1}
   ```
   *Example:* Restores changes from the specified stash entry.

6. **Pop the most recent stash**:
   ```bash
   git stash pop
   ```
   *Example:* Restores the most recent stash entry and removes it from the stash list.

7. **Drop a specific stash**:
   ```bash
   git stash drop stash@{0}
   ```
   *Example:* Deletes the specified stash entry from the stash list.

8. **Clear all stashes**:
   ```bash
   git stash clear
   ```
   *Example:* Permanently removes all stashed entries.
   
---

