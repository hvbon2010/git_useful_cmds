# Git clone
`git clone url`

Example: `git clone git@github.com:hvbon2010/git_useful_cmds.git`

# Git checkout, pull, cherry-pick
`Checkout`    : Fetches the latest changes. You should already have this repo downloaded. It does not merge those new changes but makes your working
                directory reflect them. And a name-less commit is created to include these changes in your working directory. And a detached HEAD pointing to it. You can merge them at your leisure later.

`Pull`        : Fetches the changes AND merges them into the local branch of the same name.

`Cherry-pick` : Fetches the commit and plays it on top of the current local branch, thus creating an entirely new commit which happens to have same changes
                as the one it fetched.

# Git status
List all changed files in a git project.

Git status in a subfolder only:

`cd path\to\folder ; git status .`

# Create git patch for specific commit
`git format-patch -1 <commit_sha>`

# Edit a commit
`git commit --amend`

# Commit a new patch without edit
`git commit --amend --no-edit`

# Revert a folder
`cd path\to\folder ; git checkout -- .`

# Remove a file from a commit (do not push yet)
`git reset HEAD path\to\file`

# Reset a modified file or deleted file (do not add to commit yet)
`git checkout HEAD path\to\file`

# Merge conflict binary files
Git checkout accepts an --ours or --theirs option for cases like this. So if you have a merge conflict, and you know you just want the file from the branch you are merging in, you can do:

To use that version of the file.

`git checkout --theirs -- path/to/conflicted-binary-file`

Likewise, if you know you want your version (not the one being merged in) you can use:

`git checkout --ours -- path/to/conflicted-binary-file`

# Git rebase for merger conflict process
Solution 1:

Step 1: Checkout for latest commit.

Step 2: Cherry-pick to your commit.

Step 3: Resolve all merge conflict files.

Step 4: Git add changed files.

Step 5: Git commit --amend --no-edit.

Step 6: Git rebase.

Step 7: Git push.

Solution 2:

Step 1 - Step 3: ( = Solution 1).

Step 4: git cherry-pick --continue.

Step 5: git push.

# Git cherry-pick local
Step 1: cherry-pick this commit to new branch.

Step 2: resolve all conflict files and add changed files.

Step 3: Clear the change ID in commit message.

Step 4: Git push.

