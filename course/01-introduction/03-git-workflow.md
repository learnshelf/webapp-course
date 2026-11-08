# 1.3: Git workflow

About 20 minutes. Do this right after lesson 1.2.

By the end of this lesson you will have saved your first web page with git, read exactly what changed in a file, and undone a mistake. You will also have a routine that you can repeat whenever you want to save your work.

## The idea

In [lesson 1.1](01-git-introduction.md) you saved a README. Now you have a real page to save. Whenever you want to save your work, you make the same moves:

```
  1. git status             what changed?
  2. git diff               what exactly changed?
  3. git add .              put everything that changed in the frame
  4. git commit -m "..."    take the photo, with a caption
  5. git log --oneline      check that the new save point is there
```

The dot in `git add .` means "everything in this folder that changed".

The caption says what you saved. For your first page, use the lesson number and its name, like `1.2 Hello, HTML and CSS`. After that, write a short caption that says what changed.

One thing to know about `git diff`: it only shows changes in files git already knows. A brand new file has nothing to compare with, so `git diff` stays quiet about it.

New words:

- **diff**: the difference between your file now and the file at the last save point.
- **log**: the list of your save points, newest first.

## Steps

### 1. See what is new

Open the terminal in VS Code and run:

```
git status
```

You should see: your two new files from lesson 1.2, listed as untracked.

```
On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        index.html
        style.css

nothing added to commit but untracked files present (use "git add" to track)
```

### 2. Save them

```
git add .
git commit -m "1.2 Hello, HTML and CSS"
```

You should see something like this:

```
[main b704d4a] 1.2 Hello, HTML and CSS
 2 files changed, 19 insertions(+)
 create mode 100644 index.html
 create mode 100644 style.css
```

The code and the numbers will be different on your computer. That is fine. (On Windows you may also see a warning about `LF will be replaced by CRLF`. Ignore it.)

### 3. Look back

```
git log --oneline
```

You should see your save points, newest at the top:

```
b704d4a (HEAD -> main) 1.2 Hello, HTML and CSS
ad98e00 Add a line to README
e29c74f Add README
```

Each line is one save point: a short code, then the caption you wrote. Yours may have more lines. `(HEAD -> main)` marks where you are now: the newest save point.

If the list is long, you may see a `:` at the bottom of the terminal. Press `q` to get out.

### 4. Change something and read the diff

Open `index.html` and change the welcome line. Use your own first name:

```html
<p>Hello, Sam</p>
```

Save the file, then run:

```
git diff
```

You should see:

```
diff --git a/index.html b/index.html
index eb72d2e..84bf0e4 100644
--- a/index.html
+++ b/index.html
@@ -9,7 +9,7 @@
 <body>
     <main>
         <h1>Student Planner</h1>
-        <p>Welcome, Sam</p>
+        <p>Hello, Sam</p>
     </main>
 </body>
 </html>
```

Read it like this:

- A line that starts with `-` is a line that was removed. A line that starts with `+` is a line that was added. In the terminal they are red and green.
- The lines with no sign are just there to show where the change is.
- You can ignore the lines at the top, like `@@ -9,7 +9,7 @@`, for now.

So git is telling you: the line `Welcome, Sam` was replaced by `Hello, Sam`.

### 5. Do it with the Source Control tab

Open the Source Control tab (the icon with the branching line, or Ctrl+Shift+G).

You should see: `index.html` under **Changes**, with an `M`.

Click the file name. A new tab opens, called `index.html (Working Tree)`, and it shows the diff. The left side is your last save point, and the right side is your file now. Red and green mark what is different. If your window is narrow, VS Code may put the two versions one above the other instead.

```
+--------------------------------+--------------------------------+
| last save point                | index.html (Working Tree)      |
+--------------------------------+--------------------------------+
|     <h1>Student Planner</h1>   |     <h1>Student Planner</h1>   |
| -   <p>Welcome, Sam</p>        | +   <p>Hello, Sam</p>          |
|     </main>                    |     </main>                    |
+--------------------------------+--------------------------------+
```

Now save it: hover over the file and click the **+**, type `Change the welcome word` in the message box, and click **Commit**.

Check it in the terminal:

```
git log --oneline
```

You should see: your new save point at the top. The terminal and the tab make the same kind of save point.

### 6. Undo a mistake

Delete the whole `<p>Hello, Sam</p>` line from `index.html`. Save, and look at the browser: the welcome line is gone.

Look at the Source Control tab and click the file. The diff shows the deleted line in red.

Now bring it back. Hover over `index.html` in the tab and click the **Discard Changes** icon (a curved arrow). VS Code asks you to confirm. Confirm it.

You should see: the line is back in the file, and the page in the browser shows it again. If the page has not updated, refresh it by hand.

```
  last save point ---- you edit ---- you edit more ----> now
        |                                                 |
        +---- Discard Changes: back to the last save -----+
```

The typed version of this is:

```
git restore index.html
```

Be careful with this one. Discard throws away every change in that file since the last save point, and git cannot give them back. That is why you commit often: a save point is something you can always return to.

### 7. Put the welcome back

The next lessons expect your page to say `Welcome, Sam`, so put it back the way it was before step 4. Change `Hello, Sam` back to `Welcome, Sam` and save. Then make the same moves in the terminal:

```
git status
git diff
git add .
git commit -m "Put the welcome back"
git log --oneline
```

You should see: `git diff` shows `Hello` replaced by `Welcome`, the opposite of step 4, and `Put the welcome back` at the top of the log.

## Recap

- To save your work you do the routine: `status`, `diff`, `add .`, `commit`, `log`.
- From now on, finish every lesson with the routine. Use the lesson number and its name as the caption.
- `git diff` shows what changed, line by line: `-` was removed, `+` was added.
- `git log --oneline` lists your save points.
- Discard Changes (or `git restore <file>`) takes a file back to its last save point. It cannot be undone.

```
  in the terminal            in the tab
  -----------------------    ----------------------------------------
  git status                 the lists: Changes and Staged Changes
  git diff                   click a file to see the diff
  git add .                  the + next to Changes
  git commit -m "words"      type the words in the box, click Commit
  git log --oneline          (in the terminal)
  git restore <file>         the Discard Changes icon
```

## Homework

First, finish the homework from lesson 1.2 and save it with the routine. Use the caption `1.2 Homework`. Then take it out again, as the end of each task in lesson 1.2 says, so your files match the lessons that come next.

Then try these. Each should take about five minutes.

1. **Three changes, three save points.** Make three small changes to your page, such as your name, the welcome word, or the side the text sits on (`text-align`). Save each one with its own commit. Use the terminal for two of them and the tab for one. You know it worked when `git log --oneline` shows three new captions. Take it out again when you are done: put the welcome line back to `Welcome, Sam` (with your name) and `text-align` back to `center`.

2. **Say it before you save it.** Make one more change. Before you commit, run `git diff` and say out loud, in one sentence, what it shows. Use that sentence as your caption. You know it worked when someone could understand your caption without opening the file. Take it out again when you are done, the same way as in task 1.

3. **Stretch: break it and bring it back.** Delete half of `style.css` and look at the browser to see what happens. Then bring the file back with `git restore style.css`. You know it worked when the page looks right again.

## Stuck?

- **`git diff` shows nothing.** Check that you saved the file. If the file is brand new, `git diff` skips it: use `git status` instead. If you already ran `git add` on the file, it is in the frame, and plain `git diff` only looks at changes that are not in the frame: run `git diff --staged` to see those.
- **The terminal shows a `:` and does not move on.** Press `q`.
- **You discarded something you wanted.** Git cannot bring it back. Try Ctrl+Z in the editor, and tell your teacher. Next time, commit before you experiment.
- **`nothing to commit, working tree clean`.** There is nothing new to save. Check that you saved your files.
