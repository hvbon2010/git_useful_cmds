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

# Git branch
List all branchs of git project:

`git branch -a`

# Create git patch for specific commit
`git format-patch -1 <commit_sha>`

# Apply patch
`git apply patch.diff`

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

# Gerrit push commit
`git push <abc/xyz> HEAD:refs/for/<branch>`

Example: `git push origin HEAD:refs/for/rvc-wear-dev-sw5100`

Git push private commit:

`git push <abc/xyz> HEAD:refs/for/<branch>%private`

Git push remove private status:

`git push <abc/xyz> HEAD:refs/for/<branch>%remove-private`

Git push commit with a topic:

`git push <abc/xyz> HEAD:refs/for/<branch>%topic=abc`

OR:

`git push <abc/xyz> HEAD:refs/for/<branch> -o topic=abc`

# Get history of a file
`git log -p -- [path_to_file]`

# Change author for CL pushed
`git commit --amend --reset-author --no-edit`

`git push <abc/xyz> HEAD:refs/for/<branch>`

# Log reserved
This is very useful to get the first commit.

`git log --reverse`

# Undo "git commit --amend" instead "git commit"
`git reset --soft HEAD@{1}`

# Git push to upstream branch
`git checkout -b [branch_name] upstream/branch_name`

`git commit -m ...`

`git push upstream fossil_dev`

# Git commit from one branch to another
Step 1: fetch all branch to local.

Step 2: Checkout to another branch.

Step 3: Run `git reflog` to get the commit id you want to cherry-pick.

<img width="1022" alt="image" src="https://user-images.githubusercontent.com/32226325/212032460-7400d4b4-9574-4d16-baa4-cf534c011088.png">

Step 4: Git cherry-pick commit ID to current branch.

`git cherry-pick [CID]`

`git status`

<img width="1101" alt="image" src="https://user-images.githubusercontent.com/32226325/212032358-9f17b320-21d2-4ce3-a416-e8c0af8c4a39.png">

Step 5: Git push to desired branch

`git push ...`

# Git diff ignore end of line
`git diff  --ignore-space-at-eol`

# Check authen key when authen failed
`ssh -vvv [server_addr] -i /path/to/authen_key`
