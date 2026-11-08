# 1.1: Git introduction

About 18 minutes. No web page yet.

By the end of this lesson you will have a project folder that git is watching, with two save points in it. You will have made one with typed commands and one with VS Code's Source Control tab:

```
studentplanner/
  .git/         <- git's hidden notebook, where it keeps your save points
  README.md     <- your project's front page
```

## The idea

Think of a video game. You play for a while, reach a good spot and save. If something goes wrong later, you go back to your save.

Git does the same for your whole project. The difference: you decide when to save, and you give every save a name.

A save takes two moves, like taking a photo:

1. **add**: choose what goes in the frame.
2. **commit**: take the photo, and write a caption.

```
  +-------------+  git add  +-------------+  git commit  +----------------+
  | README.md   | --------> | README.md   | -----------> | "Add README"   |
  +-------------+           +-------------+              +----------------+
   your folder               the frame                    the photo album
```

Git runs on your own computer, so it works without internet. (GitHub is a website, and a different thing. You will meet it in [lesson 1.6](06-github.md).)

Words to remember:

- **repository**: a project folder that git is watching.
- **commit**: a save point, and also the act of making one.
- **staged**: in the frame, ready to be committed. VS Code uses this word.
- **terminal**: a place where you type instructions to the computer instead of clicking.

## Steps

### 1. Make the project folder

Create a new folder called `studentplanner` somewhere you will find it again, such as Documents.

Open VS Code (short for Visual Studio Code). If you are reading this lesson in VS Code already, choose File > New Window first, so the lesson stays open in the old window. In the new window, choose File > Open Folder..., then pick that folder.

VS Code may ask "Do you trust the authors of the files in this folder?". It is your own folder, so click **Yes, I trust the authors**.

You should see: the name STUDENTPLANNER at the top of the Explorer panel on the left, with nothing inside it yet.

### 2. Open the terminal

In VS Code choose Terminal > New Terminal. (The shortcut is Ctrl and the backtick key.)

You should see: a panel at the bottom of the window, with a line that contains `studentplanner`. That is the folder you are in. The line ends with a sign (`>` on Windows, `%` on a Mac), and you type after it.

```
+--------------------------------------------------------+
| File  Edit  Selection  View  ...  Terminal  Help       |
+--------------+-----------------------------------------+
| EXPLORER     |                                         |
|              |   the editor: your files open here      |
| STUDENTPLAN  |                                         |
|              |                                         |
|              +-----------------------------------------+
|              | TERMINAL                                |
|              | ...\studentplanner>  <- you type here   |
+--------------+-----------------------------------------+
```

### 3. Check that git is there

```
git --version
```

You should see: something like `git version 2.43.0`. Your number will differ.

If you see an error such as "not recognized" or "command not found", tell your teacher before going on.

On a Mac, a window may open and offer to install the "command line developer tools". Click **Install**, wait until it says it is done (it can take a few minutes), then run `git --version` again.

### 4. Write the README

In the Explorer, click the New File icon, name the file `README.md`, and type this:

```
# Student Planner

A planner for my schedule, homework and activities.

By <your name>
```

Replace `<your name>` with your real name, without the `<` and `>`.

The `#` at the start makes a heading. A README is the front page of a project: anyone who opens the project reads it first. The `.md` stands for Markdown: plain text with a few signs, such as `#`, that turn into headings and lists when GitHub shows the file.

Save the file with Ctrl+S (Cmd+S on a Mac). A dot next to the file name in its tab means it is not saved yet.

You should see: `README.md` in the Explorer.

### 5. Tell git to watch the folder

```
git init -b main
```

`-b main` gives your timeline its name, `main`. It needs git 2.28 or newer, and any git installed in the last few years is newer than that. If git says it does not know `-b`, run `git init`, and then `git branch -M main`.

You should see: a line that starts with `Initialized empty Git repository in` and ends with `.git/`. If grey lines that start with `hint:` appear above it, they are harmless: ignore them.

Your folder now has a hidden `.git` folder. You will not see it in the Explorer. Leave it alone: if you delete it, your save points are gone.

### 6. Ask git what it sees

```
git status
```

You should see:

```
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        README.md

nothing added to commit but untracked files present (use "git add" to track)
```

"Untracked" means git can see the file but is not saving it yet. `main` is the name of your timeline. (Git's own word for a timeline is **branch**, so you will see that word in git's messages.) If it says `master` instead, run `git branch -M main` to rename it. Nothing is lost, because you have no save points yet.

### 7. Put the file in the frame

```
git add README.md
```

You should see: nothing. That is normal. Git stays quiet when a command works. (On Windows you may see a warning about `LF will be replaced by CRLF`. LF and CRLF are two ways of marking the end of a line, and the warning is harmless: ignore it.)

Now ask again:

```
git status
```

You should see:

```
On branch main

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   README.md
```

README.md moved from "untracked" to "to be committed". It is in the frame.

### 8. Take the photo

First, tell git who you are. Git puts your name and email on every save point. You do this once on each computer, and never again:

```
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

Use your own name, and the email address of your GitHub account. You should see: nothing, because git stays quiet when a command works.

Now take the photo:

```
git commit -m "Add README"
```

`-m` is for message. The words in quotes are the caption. A good caption is short and says what changed.

You should see something like this:

```
[main (root-commit) 3f2a9c1] Add README
 1 file changed, 5 insertions(+)
 create mode 100644 README.md
```

The letters and numbers in the first line will be different on your computer. That is fine.

### 9. Check that it worked

```
git status
```

You should see:

```
On branch main
nothing to commit, working tree clean
```

"Clean" means everything is saved and nothing is waiting. You have your first save point.

### 10. Do it again with buttons

VS Code has a tab that does the same job as these commands. Open it by clicking the icon with the branching line in the bar on the far left, or press Ctrl+Shift+G.

Right now there is nothing to save, so the tab is empty. Give it something: add one more line to the end of `README.md`:

```
Started this project today.
```

Save the file with Ctrl+S.

You should see: a 1 on the tab's icon, and `README.md` listed under **Changes** with an `M` beside it. `M` means modified: git already knows the file, and it has changed. (A brand new file shows a `U` instead, for untracked.) This list is `git status`, drawn as a picture.

```
+-----------------------------------+
| SOURCE CONTROL                    |
|                                   |
| [ Message                       ] |
| [            Commit             ] |
|                                   |
| v Changes                       1 |
|     README.md             [+]  M  |
+-----------------------------------+
```

Next, put the file in the frame. Hover over `README.md` and click the **+** that appears.

You should see: `README.md` moves to **Staged Changes**. "Staged" is the tab's word for "in the frame".

```
+-----------------------------------+
| SOURCE CONTROL                    |
|                                   |
| [ Message                       ] |
| [            Commit             ] |
|                                   |
| v Staged Changes                1 |
|     README.md             [-]  M  |
+-----------------------------------+
```

Last, take the photo. Click the Message box, type `Add a line to README`, and click **Commit**.

You should see: both lists empty, because everything is saved.

```
+-----------------------------------+
| SOURCE CONTROL                    |
|                                   |
| [ Message                       ] |
| [            Commit             ] |
|                                   |
|  (the lists are empty)            |
+-----------------------------------+
```

Your tab will look a little different from these sketches, but it has the same parts. Check in the terminal:

```
git status
```

You should see: `nothing to commit, working tree clean` again.

The terminal and the tab are two ways of doing the same thing:

```
  in the terminal          in the tab
  ----------------------   ----------------------------------------
  git status               the lists: Changes and Staged Changes
  git add <file>           the + next to a file
  git commit -m "words"    type the words in the box, click Commit
```

## Recap

- A commit is a save point with a name.
- Saving takes two moves: `git add` picks what goes in the frame, and `git commit` takes the photo.
- `git status` tells you where things stand. Use it often.
- The Source Control tab does the same with buttons: **Changes** are the files that changed, **Staged Changes** are the files in the frame, and **Commit** takes the photo.

```
git init -b main         start watching this folder (once per project)
git status               what has changed? what is saved?
git add <file>           put a file in the frame
git commit -m "words"    take the photo, with a caption
```

Next you will build your first web page, in [lesson 1.2](02-hello-html-css.md). After that you will learn to look back at your save points.

## Homework

Do these in the same project. Each should take about five minutes.

1. **With the terminal.** Add a line to `README.md` about something you want to learn, and save the file. Run `git status`: it lists `README.md` as modified. Add it, commit it with your own caption, and run `git status` again. You know it worked when it says "working tree clean".

2. **With the tab.** Create `notes.md` with three things you would like to build or learn. Save it and look at the Source Control tab: the new file has a `U`. Stage it, then commit it with the caption `Add notes`. You know it worked when the tab's lists are empty.

3. **Stretch: choose what goes in the frame.** Change `README.md` and also add a line to `notes.md`. Save both. In the tab, stage `README.md` only. You will see two lists, each with one file. Commit, then look at the tab again: which file is still waiting, and why? Then stage it and commit it too. You know it worked when `git status` in the terminal says "working tree clean".

## Stuck?

- `fatal: not a git repository`: the terminal is not in your project folder, or you have not run `git init`. Check that the line contains `studentplanner`, then run `git init -b main`.
- `no changes added to commit`: you changed a file that git already knows, and skipped `git add`. Run `git add <file>`, then commit again.
- `nothing added to commit but untracked files present`: you made a new file and skipped `git add`. Run `git add <file>`, then commit again.
- `Author identity unknown`: git does not know your name yet. Run the two `git config --global` lines from step 8, then commit again.
- A long note that says `Your name and email address were configured automatically` (often on a Mac): git made up a name from your computer, because you skipped the two `git config --global` lines in step 8. Run them now, then run `git commit --amend --reset-author --no-edit` to fix the save point you just made.
- A text editor opened after `git commit`, or the terminal shows a `>` and does not move on: you left out `-m`, or you left out a closing quote. For the editor, press Esc, type `:q!` and press Enter (if a VS Code tab opened instead, close it). For the `>`, press Ctrl+C. Then type the commit line again.
- A file called `.DS_Store` is listed as untracked (a Mac): Finder leaves it in folders. It is harmless. Do not add it by name.
- The Source Control tab says the folder does not have a git repository: you have not run `git init` yet (step 5), or you opened a different folder.
- VS Code asks something like "There are no staged changes to commit. Would you like to stage all your changes and commit them directly?": you clicked Commit before staging anything. Cancel, stage the file with the **+**, then commit.
