How does git store info?
Key value store
Key = hashed SHA1 Data
Data = Data 

Compressed data = Blob(contains header blob along with the size and the data)
Blobs are generally unique this is helpful for lots of things

Blobs are stored in threes because 
Blobs missing information... Filenames, directory structures,
Threes contains pointers to Blobs or other threes and metadata (type (blob, three) filename or directory name, mode)

Git doesnt store empty directories

Why SHA1 is useful:
Identical content is only stored once 
Security
No forges
Preventing corruption

git compress data and stores deltas or the difference between versions.

Commits:
Points to a tree 
Metadata: author, committer, data, message, parent commits
SHA1= all of the above information hash
we cant change commits because the sha1 will change if you change anything from the object

git-ct-file -t type
git-ct-file -p print

References
Tags, Branches, HEAD
changing branches is as simple as changing a pointer, so it is actually fast.

Working area = untracked files
Staging area = What files are going to be part og the next commit
How git knows what will change between the current commit and the next commit
git ls-files -s -> MODE, SHA, filename 
commands: git add, git rm, git mv
git add-p: unstaging files (replacing them with something at the repository) 
Repository = Every commit
Stash = Temporary save your staging area
stash --all includes untracked files
stash save names for easier references
stash branch from a stash
git checkout stashname --filename Grab a single file from a stash (overwrites the file)
stash clear pop, unstash work
stash drop delete latest stash
stash clear clears every stash
REFERENCES
Tags & Annotated Tags
Lightweights: pointer to a commit
Annotated: pointer to a commit with additional information, author, message, date
Commits that a tag points to doesnt change 

Branches
pointer to a particular commit 
the current branch pointer moves with every commit to the repository

HEAD
current branch, parent of the next commit (keep versions going)
usually points to the name of the current branch
it can point to a commit
it moves when 
you make a commit ion the currently active branch
when you checkout a new branch

DETACHED HEAD
When you checkout a specific commit or a tag instead of a branch HEAD-LESS state
Head points to that commit
if you dont do anything to that commit you may lose your work, then you can
*create a new branch that points to the last commit 
git branch branchname commit 
** discard your work and wait for the garbage collector to fully delete them

MERGE & REBASE
Merge commits are commits that have more than one parent
Fast forward clear path from the tip of the current branch to the tip of the target branch 
When after branching our feature there were no more new commits to master so we can just add our commits to master and change the head 
You can avoid that with merge --no-ff 
in order to have a merger commit avoiding fast forward 

RERERE reuse recorded resolution
git config rerere.enabled true
if the same conflict happens git will use the same resolution

Commit messages:
Be verbose about your changes
Good commits:
Dont let your code in a broken state

Git log 
--since "yesterday", "2 weeks ago"
--follow changes history
--diff-filter Added, Deleted, modified, etc
the hat ^ and tilde ~ for  referencing commit
the hat references the nth parent commit
the tilde references the n of commits back

git show commit        : show commit and contents
                --stat : files changed
                :file  :llok at a file from another commit 

git diff: shows you changes between commits, between the staging area and the repo, whats in the working area
for unstaged changes: git diff
for staged changes: gt diff --staged

FIXING MISTAKES
Checkout
Restore working tree files or witch between branches
--FILE: replace the working are copy with the version from the current staging area from the last commit
commit --file: update the staging area to match the commit  and updates the working are to match the staging area
we can use git checkout to restore a deleted file
git checkout deleting_commit -- filepath
Reset
Moves the head and the branch reference 
can change history 
git reset --mixed by default

with a path
Does not move the head pointer, modifies files
without a path

--soft :just moves the head pointer
--mixed :moves the head and copies the file from the commit is pointing to 
--hard: moves head, and copies the file from the commit to the staging and working area it overrides whatever you have on your working area

Revert
"SAFE RESET"
creates a new commit that introduces the opposite changes from one specified commit

Clean
Cleans your working area deleting untracked files
-d: will clean directories
--dry-run to see what would be deleted

AMEND
Shortcut that lets you make changes to the previous commit
git commit --amend 
creates a new commit with the "merge" of the changes

REBASE
Gie a commit a new parent or a new "Base" commit
First Rewinds head
Creates a copy of the current commit 
this makes resolving merge conflicts easier
it allows us to edit, remove, combine, re-order and insert commits 
before theyre on top of the new HEAD
-i : interactive rebase
options
pick reword edit squash fixup exec drop

Amend commit with fixup & autosquash
git commit --fixup SHA
git rebase -i --autosquash SHA

before rebasing/fixup/squash/reorder
make a copy of the current branch 
git branch backup_branch
in case the rebase goes wrong
git reset backup_branch --hard

ABORT
--abort cancels it (what a surprise)

You store the whole repository and history at your local machine that means it is a DISTRIBUTED VERSION CONTROL

GITHUB:
Repository host
browse code
issues
prs
forks: copy of a repository a your gh account 

REMOTE
is a git repository stored elsewhere, on the web, cloud, github etc
FETCH 
it pulls down all the changes that happened on the server but it doesnt change your local repo
PULL 
git fetch and merge
--rebase builtin rebase (don't use if you have local merge commits)
PUSH
send changes to the repository
--rebase builtin rebase

TAGS
You have to push tags to the repo

CONTINUOUS INTEGRATION
merging smaller commits more frequently, divide and conquer
run tests before merging 

GIT HUB API
un auth: 60 request per hour
personal token: testing personal projects, API implementations, etc
OAuth: The user will login via OAuth in the project
via APi you can create and update Issues PRs, Repos, Gists 



