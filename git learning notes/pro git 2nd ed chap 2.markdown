
CHAPTER 2 - GIT BASICS
skills;
    -config and initialize a repo
    -begin and stop file tracking
    -stage and comit changes
    -setup git to ignore files and file patterns
    -undo mistakes quick and ez, browse history of project, view changes between commits, push and pull from remote repos

Getting a git repo
-taking an existing project/directory and importing into git
-clone an existing git repo from another server

INITIALIZING A REPO IN AN EXISTING DIRECTORY

-when starting to track existing project, go to repo and type;
    git init
creates new subdirectory named .git - repo files/skeleton
-nothing tracked yet
-do initial commit to begin tracking
'
git add *.c
git add LICENSE
git commit -m 'initial project version'
'
this gives you a git repo with tracked files and an initial commit

CLONING AN EXISTING REPO

git clone - clones a repo
-git receives full copy of nearly all data the server has
-every file ver is pulled
-if server gets corrupted, can use any of the client clones to reset server (all versioned data)

'git clone [url]'
i.e.
git clone https://github.com/libgit2/libgit2

-created dir named 'libgit2', initializes .git dir inside it, pulls all data for repo, checks working copy of latest ver
-all working files ready in dir
0can specify dir location in next cli option

git clone https://github.com/libgit2/libgit2 mylibgit

-does same as prev command but target dir is called mylibgit

*git has number of transfer protocols
-can use https://, git://, user@server:path/to/repo.git (ssh)

RECORDING REPO CHANGES
tracked - files from last snapshot, in staging area,
untracked - everything else

flow;
-clone repo, files start tracked and unmodified
-as you edit, git sees them as modified
-stage modified files then commit all staged changes
-repeat cycle
-any untracked files get added once they are staged and committed

untracked => add file => staged
unmodified => edit file => modified => stage file => staged
staged => commit => unmodified => remofe file => untracked

CHECKING FILE STATUS
git status - check file status directly after a clone
On branch master
'your branch is up-to-date with 'origin/master'.
nothing to commit, working dir clean

master branch = default
=clean working directory
-git doesn't see any untracked files

echo 'My Project' > README
git status
On branch master
Your branch is up-to-date with 'origin/master'.
Untracked files:
    (use "git add <file>..." to include in what will be committed)

    README

nothing added to commit but untracked files present (use "git add" to track)

-new readme file is untracked -- under untracked files heading in status output
-untracked = file not in last snapshot
-git won't inc in commit snapshots until you tell it to

TRACKING NEW FILES
git add README (starts tracking file)

git status
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
    (use "git reset HEAD <file>..." to unstage)

    new file: README

-it's staged bc under changes to commit heading
-if you commit, ver of file at time of git add will become snapshot
-git add cmd takes path name for file or dir, if dir adds all files recursively

STAGING MODIFIED FILES
-change a file alr tracked
-if you change CONTRIBUTING.md, which was previously tracked;

git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
    (use "git reset HEAD <file>..." to unstage)

        new file: README
Changes not staged for commit:
    (use "git add <file>..." to update what will be committed)
    (use "git checkout -- <file>..." to discard changes in working directory)
    modified: CONTRIBUTING.md


-file is not staged
-to stage, run git add
-used to begin tracking new files, stage files, mark merge conflictd files as resolved
-'add this file to next commit' >> add file to project

running git add now to stage CONTRIBUTING.md file, then git status;

git add CONTRIBUTING.md
git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
    (use "git reset HEAD <file>..." to unstage)

    new file: README
    modified: CONTRIBUTING.md

-both files staged > go to next commit
i.e. rmb one more change to CONTRIBUTING.md, make change then git status;

vim CONTRIBUTING.md
git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
    (use "git reset HEAD <file>..." to unstage)

        new file: README
        modified: CONTRIBUTING.md

Changes not staged for commit:
    (use "git add <file>..." to update what will be committed)
    (use "git checkout -- <file>..." to discard changes in working directory)
    modified: CONTRIBUTING.md

-git uploads snapshot of file from when you ran git add
-if you edit a file after git add, need to do git add again before commit to stage latest version of file

git add CONTRIBUTING.md
git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
    (use "git reset HEAD <file>..." to unstage)
        new file: README
        modified: CONTRIBUTING.md

