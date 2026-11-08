# Git cheatsheet

The git commands you need, on one page.

## The picture

```
  files --git add--> frame --git commit--> save points --git push--> GitHub
```

- **add** puts changed files in the frame.
- **commit** takes the photo: a save point with a caption.
- **push** sends your save points to GitHub.

## Once per computer

Git puts your name and email on every save point, so tell it who you are. Use the email address of your GitHub account:

```
git config --global user.name "Your Name"          your name
git config --global user.email "you@example.com"   your email
```

## Once per project

```
git init -b main                      start watching this folder
git remote add origin <address>       tell git where the copy lives
git push -u origin main               the first push, to set it up
```

`-b main` names your first timeline `main`. It needs git 2.28 or newer. If git does not know `-b`, run `git init`, then `git branch -M main`.

To start from a copy that is already on GitHub, copy it to your computer once. Git makes a folder with the project's name:

```
git clone <address>                   copy a project from GitHub to your computer
```

## The routine

```
git status                what changed?
git diff                  what exactly changed?
git add .                 put everything that changed in the frame
git commit -m "words"     take the photo, with a caption
git log --oneline         check the new save point is there
git push                  send it to GitHub
```

The caption says what you saved, in a few words, like `Change the welcome word`.

## Looking around

```
git --version             is git installed?
git status                what changed? what is saved?
git diff                  the changes that are not in the frame yet
git diff --staged         the changes that are in the frame
git log --oneline         your save points, newest first
git remote -v             where does the copy live?
```

`git diff` shows nothing for a file that you have already added. Use `git diff --staged` to see it. A brand new file shows in `git status` only.

If the log does not end by itself and you see a `:`, press `q`.

## Saving one file

```
git add <file>            put just one file in the frame
```

Use it instead of `git add .` when you only want to save one file. Then commit as usual.

## Getting new save points

```
git pull                  bring new save points from GitHub to your computer
```

Use it when the copy on GitHub is ahead of your computer, for example after you pushed from another computer.

## Undo

```
git restore <file>             take a file back to its last save point
git restore --staged <file>    take a file out of the frame (it keeps its changes)
```

Be careful with the first one. It throws away every change in that file since the last save point, and git cannot give them back. The second one only takes the file out of the frame, and your changes stay.

## In VS Code: the Source Control tab

Open it with the icon with the branching line, or Ctrl+Shift+G.

```
  in the terminal            in the Source Control tab
  -----------------------    ---------------------------------------
  git status                 the lists: Changes and Staged Changes
  git diff                   click a file to see the diff
  git add .                  the + next to Changes
  git commit -m "words"      type the words in the box, click Commit
  git push                   the Sync Changes button
  git restore <file>         the Discard Changes icon
```

A letter beside a file says what happened to it: `M` is modified, and `U` is untracked, a new file that git is not saving yet.

## When something goes wrong

- `fatal: not a git repository`: the terminal is not in your project folder, or you have not run `git init -b main`.
- `no changes added to commit`: you changed a file that git already knows, and skipped `git add`. Add the file, then commit again.
- `nothing added to commit but untracked files present`: you made a new file and skipped `git add`. Add the file, then commit again.
- `Author identity unknown`: git does not know your name yet. Run the two `git config --global` lines under "Once per computer", then commit again.
- `Your name and email address were configured automatically`: git made up a name from your computer. Run the two `git config --global` lines, then run `git commit --amend --reset-author --no-edit` to fix the save point you just made.
- A text editor opened after `git commit`: you left out `-m`. Press Esc, type `:q!` and press Enter. If a VS Code tab opened instead, close it. Then run the commit again with `-m "words"`.
- The terminal shows a `>` and does not move on: a quote was opened and never closed. Press Ctrl+C, and type the line again.
- `fatal: remote origin already exists`: the remote is already set. Check it with `git remote -v`. To fix a wrong address, run `git remote set-url origin <the right address>`.
- `error: src refspec main does not match any`: your timeline has a different name, or you have not saved anything yet. Run `git status`. If it says `master`, run `git branch -M main` and push again.
- `Authentication failed` or `Permission denied`: GitHub does not know it is you. Sign in again when a window asks, check that it is your own account, and check the address with `git remote -v`. If it still fails, read the message again and ask someone you trust to look at it with you.
- `Updates were rejected because the remote contains work that you do not have locally`: the copy on GitHub has work that your computer does not have. Read the message again, run `git status`, and ask someone you trust to look at it with you before you go on. Do not use `--force`.
- A file called `.DS_Store` is listed as untracked (a Mac): Finder leaves it in folders. It is harmless. Do not add it by name.

## Words

- **repository**: a project folder that git is watching.
- **commit**: a save point, and also the act of making one.
- **staged**: in the frame, ready to be committed.
- **untracked**: a file that git can see but is not saving yet.
- **working tree clean**: everything is saved, and nothing is waiting.
- **diff**: the difference between your file now and the file at the last save point.
- **log**: the list of your save points.
- **branch**: git's name for a timeline. Your first one is called `main`.
- **remote**: a copy of your project kept somewhere else. Its usual nickname is `origin`.
- **push**: send your new save points to the remote.
