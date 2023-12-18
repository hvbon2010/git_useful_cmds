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

Git add reviewer

`git push <abc/xyz> HEAD:refs/for/<branch>%r=a@gmail.com,r=b@gmail.com`

# Get history of a file
`git log -p -- [path_to_file]`

`git log --follow [path_to_file]`

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

For Example with github:
`ssh -vvv git@github.com -i ~/.ssh/id_ed25519_github`

```
Hi hvbon2010! You've successfully authenticated, but GitHub does not provide shell access.
debug2: channel 0: written 91 to efd 6
debug3: channel 0: will not send data after close
debug2: channel 0: obuf empty
debug2: chan_shutdown_write: channel 0: (i3 o1 sock -1 wfd 5 efd 6 [write])
debug2: channel 0: output drain -> closed
debug2: channel 0: almost dead
debug2: channel 0: gc: notify user
debug2: channel 0: gc: user detached
debug2: channel 0: send close
debug3: send packet: type 97
debug2: channel 0: is dead
debug2: channel 0: garbage collecting
debug1: channel 0: free: client-session, nchannels 1
debug3: channel 0: status: The following connections are open:
  #0 client-session (t4 r43 i3/0 o3/0 e[write]/0 fd -1/-1/6 sock -1 cc -1 io 0x00/0x08)

debug3: send packet: type 1
Connection to github.com closed.
Transferred: sent 3044, received 3132 bytes, in 0.6 seconds
Bytes per second: sent 5315.5, received 5469.2
debug1: Exit status 1
```

# Git auto add changeID for all commits (for gerrit with automaticcally insert a Change-ID)
When you push more commits but failed, ex
```
Enumerating objects: 222, done.
Counting objects: 100% (222/222), done.
Delta compression using up to 48 threads
Compressing objects: 100% (131/131), done.
Writing objects: 100% (173/173), 34.64 KiB | 17.32 MiB/s, done.
Total 173 (delta 125), reused 62 (delta 33), pack-reused 0
remote: Resolving deltas: 100% (125/125)
remote: Counting objects: 185121, done
remote: Processing changes: refs: 1, done    
remote: ERROR: commit d8950e4: missing Change-Id in message footer
remote: 
remote: Hint: to automatically insert a Change-Id, install the hook:
remote:   gitdir=$(git rev-parse --git-dir); scp -p -P 5222 hvbon@gerrit-asia.fossil.com:hooks/commit-msg ${gitdir}/hooks/
remote: (for OpenSSH >= 9.0 you need to add the flag '-O' to the scp command)
remote: or, for http(s):
remote:   f="$(git rev-parse --git-dir)/hooks/commit-msg"; curl -o "$f" https://gerrit-asia.fossil.com/tools/hooks/commit-msg ; chmod +x "$f"
remote: and then amend the commit:
remote:   git commit --amend --no-edit
remote: Finally, push your changes again
remote: 
To ssh://gerrit-asia.fossil.com:5222/unicorn/zephyr/zephyr
 ! [remote rejected]       HEAD -> refs/for/main-bes%private (commit d8950e4: missing Change-Id in message footer)
error: failed to push some refs to 'ssh://gerrit-asia.fossil.com:5222/unicorn/zephyr/zephyr
```

So, we will install the hook:

`gitdir=$(git rev-parse --git-dir); scp -p -P 5222 hvbon@gerrit-asia.fossil.com:hooks/commit-msg ${gitdir}/hooks/`

`f="$(git rev-parse --git-dir)/hooks/commit-msg"; curl -o "$f" https://gerrit-asia.fossil.com/tools/hooks/commit-msg ; chmod +x "$f"`

And then, ammend for HEAD commit by command:

`git commit --amend --no-edit`

But if we have more older commits which don't have changeID, we will run commands:

`git rebase -f <commit_id_no_change_id>~1 <branch_name> --exec "git commit --amend --no-edit"`

And push again.

# Git update an attribute for all commits in a changes (gerrit)
We have a list of commits in chains and you want add a topic, unmark private, add reviewers for all of them, how to do it.

The first, you need to rebase all of commits in a change to create a new changeID for all of them.

`git rebase -f <first_commit_id_of_commit_in_change>~1 <branch_name> --exec "git commit --amend --no-edit"`

And then push it with add topic, unmark private, add reviewers you want.
