# 3.5: One look for many

About 35 minutes.

By the end of this lesson the white box with a line and round corners is written once, as `.card`, and every box in your app uses it: the rows of the Schedule, the club cards, the sessions and the front door. You will see how a small extra class changes one card without a new set of rules, and why a name for how something looks works better than a name for where it is used.

## The idea

Lesson 3.4 took the lines that say where things go out of your classes. What is left in `style.css` is how things look. Look at it the same way. Which looks are written more than once?

```
  rule             how it looks

  .course          a white box, padding 1rem, a khaki line, round corners 8px
  .activity        a white box, padding 1rem, a khaki line, round corners 8px
  .session         a white box, padding 1rem, a khaki line, round corners 8px
  .card            a white box, padding 2rem, a red line, round corners 12px, a margin

  .course-name     bold, 1.1rem
  .activity-name   bold, 1.1rem

  .course-time     grey, typewriter letters
  .session-time    grey, typewriter letters
```

Three boxes are the same, and a fourth is nearly the same. You wrote the box in lesson 2.6 as `.card`. The name says how it looks, and nothing about what is inside, so it can be the one look for all of them. Names like `course`, `activity` and `session` say what the box holds on one page.

A class that says only how a tag looks is a **look class**. Like a place class, it is best named for what it is, not for where it is used.

A tag has several classes, so it can have a shared look, and then a small change for one tag:

```
  <div class="card roomy accent">
        |    |     |
        |    |     +-- a change: a red line
        |    +-------- a change: more room
        +------------- the shared look
```

A common way to name classes is by the parts of a thing. A card has `card`, and its parts have `card-header`, `card-content` and `card-footer`. It looks tidy, and all cards look the same. But when one card has to be different, you need new classes for it and for each of its parts. The names of the parts are tied to the card. With look classes you add one class to one tag, and the rest of the card stays as it is.

New words:

- **look class**: a class that says only how a tag looks, such as `card`.

## Steps

### 1. Start from last time

Open your project in VS Code and make sure Go Live is running. You will change four of them. `layout.css` stays as it is.

You should have `index.html`, `schedule.html`, `activities.html`, `layout.css` and `style.css`, as at the end of lesson 3.4.

Your homework may have changed your files. Take those changes out before you start, or keep a copy somewhere else, so your files match the end of the last lesson.

You should see: the front door in its card, the Schedule page with four rows, and the Activities page with three cards and four sessions.

### 2. Find the repeats

Open `style.css` and press Ctrl+F (Cmd+F on a Mac). Search for `border: 2px solid khaki`. Then search for `padding: 1rem;`.

You should see: `of 3` for both. The box is written out three times, once for each of `.course`, `.activity` and `.session`. Close the search with Escape.

### 3. One look for every box

Find the `.card` rule from lesson 2.6. Replace it with this:

```css
.card {
    padding: 1rem;
    background-color: white;
    border: 2px solid khaki;
    border-radius: 12px;
}
```

It is the look the three boxes share, with the round corners of the card.

Save, open `index.html` in the browser and look.

You should see: the front door in a smaller card, with a pale line and no room around it. The title almost touches the edges of the card, and it looks cramped. It lost the red line, the extra padding and the margin. The next step gives them back, without a second card class.

### 4. Two small changes

Add these two rules to the bottom of `style.css`:

```css
.roomy {
    padding: 2rem;
    margin: 1rem;
}

.accent {
    border-color: firebrick;
}
```

Each is one small change. `.roomy` gives more room, inside (padding) and outside (margin), and `.accent` changes the colour of the line. Now put them on the front door, beside `card`, in `index.html`:

```html
<div class="card roomy accent">
```

Save and look at the browser.

You should see: the front door as it was before this lesson: the red line, the room inside and the room around it. The two rules come after `.card` in the file. They set `padding` and `border-color` again, and when two rules disagree, the later one wins, as in lesson 2.1. That works here. In lesson 3.6 you will see why room inside a look class causes trouble.

### 5. The Schedule page

In `schedule.html`, give each row `card` in place of `course`:

```html
<li class="row align-center card">
```

Change all four rows. Then delete the `.course` rule from `style.css`, with its curly brackets. The look is in `.card` now. Keep `.course-name` and `.course-time` for now. They go in step 7.

Save and look at the browser.

You should see: the same four rows. The corners are a little rounder, 12 pixels in place of 8.

### 6. The Activities page

In `activities.html`, do the same for the clubs and for the sessions:

```html
<li class="column card">
```

```html
<li class="row align-center card">
```

The first is for each club. The second is for each session. Delete the `.activity` rule and the `.session` rule from `style.css`.

Save and look at the browser.

You should see: the same page, with a little rounder corners. Every box in your app is now a `card`.

### 7. A look for titles and times

The names and the times repeat as well: `course-name` and `activity-name` are the same, and so are `course-time` and `session-time`. Add two rules to the bottom of `style.css`:

```css
.title {
    font-size: 1.1rem;
    font-weight: bold;
}

.time {
    color: dimgray;
    font-family: "Courier New", monospace;
}
```

Use them in the pages. In `schedule.html`, the name and the time of each row become:

```html
<span class="width-fill title">Mathematics</span>
<span class="time">08:30-09:20</span>
```

In `activities.html`, the name of each club becomes `<span class="title">Chess club</span>`, and the time of each session becomes `<span class="time">15:30</span>`. The days and the times of the clubs had their own names, `activity-days` and `activity-time`, and no rule for them. Take those two names out, and keep `muted`:

```html
<span class="muted">Mondays and Thursdays</span>
<span class="muted">15:30-16:30</span>
```

Then delete the four rules you no longer use: `.course-name`, `.course-time`, `.activity-name` and `.session-time`. Keep `.session-day` and `.session-name`: they belong to one place only, the list of sessions.

Save and look at the browser.

You should see: the same pages as in step 6.

### 8. Change one card

You want the Chess club to stand out. In `activities.html`, add a class to the first club only:

```html
<li class="column card accent">
```

Save and look at the browser.

You should see: the Chess club card has the red line, and the other two have the pale one. You added one class to one tag, and wrote no new rule. The title, the days and the time of the card stayed as they are.

### 9. Count again

Press Ctrl+F (Cmd+F on a Mac) in `style.css`, and search for `border: 2px solid khaki`. Then search for `padding: 1rem;`.

You should see: `of 1` in both. They were `of 3` in step 2. The box is written once. Close the search with Escape.

### 10. Check your files

`index.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Student Planner</title>
    <link rel="stylesheet" href="layout.css">
    <link rel="stylesheet" href="style.css">
    <link rel="icon" type="image/svg+xml" href="favicon.svg">
</head>
<body>
    <main class="column align-center justify-center landing">
        <div class="card roomy accent">
            <h1>Student Planner</h1>
            <p>Welcome, Sam</p>
            <p class="tagline muted">Plan your week</p>
            <button class="btn">Continue</button>
        </div>
        <p class="muted">Made by Sam</p>
    </main>
</body>
</html>
```

`schedule.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Schedule</title>
    <link rel="stylesheet" href="layout.css">
    <link rel="stylesheet" href="style.css">
    <link rel="icon" type="image/svg+xml" href="favicon.svg">
</head>
<body>
    <header class="row justify-between align-center app-bar">
        <a class="app-name" href="index.html">Student Planner</a>
        <nav class="row">
            <a class="tab current" href="schedule.html">Schedule</a>
            <a class="tab" href="activities.html">Activities</a>
        </nav>
    </header>
    <main class="page">
        <h1>My Schedule</h1>
        <p class="muted">4 lessons, the same every day</p>
        <ul class="column">
            <li class="row align-center card">
                <span class="width-fill title">Mathematics</span>
                <span class="time">08:30-09:20</span>
                <button class="btn">Delete</button>
            </li>
            <li class="row align-center card">
                <span class="width-fill title">English</span>
                <span class="time">09:30-10:20</span>
                <button class="btn">Delete</button>
            </li>
            <li class="row align-center card">
                <span class="width-fill title">Biology</span>
                <span class="time">10:40-11:30</span>
                <button class="btn">Delete</button>
            </li>
            <li class="row align-center card">
                <span class="width-fill title">History</span>
                <span class="time">11:40-12:30</span>
                <button class="btn">Delete</button>
            </li>
        </ul>
    </main>
</body>
</html>
```

`activities.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Activities</title>
    <link rel="stylesheet" href="layout.css">
    <link rel="stylesheet" href="style.css">
    <link rel="icon" type="image/svg+xml" href="favicon.svg">
</head>
<body>
    <header class="row justify-between align-center app-bar">
        <a class="app-name" href="index.html">Student Planner</a>
        <nav class="row">
            <a class="tab" href="schedule.html">Schedule</a>
            <a class="tab current" href="activities.html">Activities</a>
        </nav>
    </header>
    <main class="page">
        <h1>Activities</h1>
        <h2>Clubs</h2>
        <ul class="grid">
            <li class="column card accent">
                <span class="title">Chess club</span>
                <span class="muted">Mondays and Thursdays</span>
                <span class="muted">15:30-16:30</span>
            </li>
            <li class="column card">
                <span class="title">Drama club</span>
                <span class="muted">Tuesdays</span>
                <span class="muted">16:00-17:30</span>
            </li>
            <li class="column card">
                <span class="title">Robotics</span>
                <span class="muted">Wednesdays</span>
                <span class="muted">15:30-17:00</span>
            </li>
        </ul>
        <h2>Coming up</h2>
        <ul class="column">
            <li class="row align-center card">
                <span class="session-day">Mon 9 Nov</span>
                <span class="width-fill session-name">Chess club</span>
                <span class="time">15:30</span>
            </li>
            <li class="row align-center card">
                <span class="session-day">Tue 10 Nov</span>
                <span class="width-fill session-name">Drama club</span>
                <span class="time">16:00</span>
            </li>
            <li class="row align-center card">
                <span class="session-day">Wed 11 Nov</span>
                <span class="width-fill session-name">Robotics</span>
                <span class="time">15:30</span>
            </li>
            <li class="row align-center card">
                <span class="session-day">Thu 12 Nov</span>
                <span class="width-fill session-name">Chess club</span>
                <span class="time">15:30</span>
            </li>
        </ul>
    </main>
</body>
</html>
```

`layout.css` did not change.

`style.css`:

```css
body {
    margin: 0;
    background-color: lightyellow;
    color: darkslategray;
    font-family: Georgia, serif;
    line-height: 1.5;
}

h1 {
    margin-top: 0;
    font-size: 3rem;
    color: firebrick;
}

p {
    font-size: 1.5rem;
}

.muted {
    color: dimgray;
    font-size: 1rem;
}

.tagline {
    font-style: italic;
    letter-spacing: 0.15rem;
    text-transform: uppercase;
}

.btn {
    background-color: #2350c8;
    color: white;
    border: none;
    border-radius: 6px;
    padding: 0.6rem 1.2rem;
    font-size: 1rem;
    font-weight: bold;
    cursor: pointer;
    transition: background-color 0.2s;
}

.btn:hover {
    background-color: #1c3f9c;
}

.btn:active {
    background-color: #142f78;
}

.landing {
    min-height: 100vh;
    text-align: center;
}

.card {
    padding: 1rem;
    background-color: white;
    border: 2px solid khaki;
    border-radius: 12px;
}

.page {
    padding: 1.5rem;
}

.app-bar {
    padding: 0.75rem 1.5rem;
    background-color: white;
    border-bottom: 2px solid khaki;
}

.app-name {
    color: firebrick;
    font-size: 1.5rem;
    font-weight: bold;
    text-decoration: none;
}

.tab {
    color: darkslategray;
    padding: 0.5rem 1rem;
    border-radius: 6px;
    text-decoration: none;
}

.tab:hover {
    text-decoration: underline;
}

.current {
    background-color: #2350c8;
    color: white;
    font-weight: bold;
}

ul {
    list-style: none;
    margin: 0;
    padding: 0;
}

.session-day {
    width: 7rem;
    font-weight: bold;
}

.session-name {
    font-size: 1.1rem;
}

.roomy {
    padding: 2rem;
    margin: 1rem;
}

.accent {
    border-color: firebrick;
}

.title {
    font-size: 1.1rem;
    font-weight: bold;
}

.time {
    color: dimgray;
    font-family: "Courier New", monospace;
}
```

### 11. Save it

Save your work with the routine, and push it. The caption is `3.5 One look for many`. The [git cheatsheet](../reference/01-git-cheatsheet.md) has the commands.

## Recap

- A look that is written more than once can be a look class. Here the white box with a line became `.card`.
- A look class is named for how it looks, such as `card`, `title` and `time`, and not for where it is used. A name like `course` ties a look to one page.
- A small change to one tag is another look class beside the shared one, such as `roomy` and `accent`. It comes after `.card` in the file, so it wins where the two disagree.
- A card with parts that have their own names, such as `card-header` and `card-footer`, looks the same everywhere. Changing one card then takes new classes for the card and for each part.
- A place class says where the children go, and a look class says how the tag looks. A tag has some of each: `row align-center card`.
- What is left in your own classes belongs to one place only, such as `.session-day`.

## Homework

Each should take about five minutes.

1. **One more look.** Write a look class `.soft { background-color: aliceblue; }` at the bottom of `style.css`. Put it on the last session: `<li class="row align-center card soft">`. You know it worked when only that row has the pale blue inside, and you wrote no rule for the row. Take `soft` off the row, and the `.soft` rule out of `style.css`, when you are done.

2. **Predict, then check.** Move the `.accent` rule above the `.card` rule. Before you save, say what colour the line on the first club card will be. Then save and look, and put it back. You know it worked when you can say why. Hint: lesson 2.1. The `border` line in `.card` sets the colour as well.

3. **Another place for the look.** Put `card` on the `nav` in the top bar in both files: `<nav class="row card">`. You know it worked when the two links sit in a box, and you wrote no CSS. On a narrow window the box may not fit, and that is fine for this exercise. Take it off again.

4. **Stretch: a bigger title.** Write `.big { font-size: 1.5rem; }` at the bottom of `style.css`. Add it to one title: `class="title big"`. You know it worked when that title is bigger and still bold, and you can say which line both classes decide, and which class wins. Then move `.big` above `.title`, and say what happens. Take `big` off the title, and the `.big` rule out of `style.css`, when you are done.

## Stuck?

- **The front door lost its look.** Check that `index.html` has `class="card roomy accent"`, and that `.roomy` and `.accent` are below `.card` in `style.css`.
- **A box has no look at all.** Check that its tag has `card` and that the rule `.card` is still in `style.css`, with the dot.
- **The red line does not show.** `.accent` must come after `.card`. The later rule wins.
- **The names are not bold.** Check that the tag has `title`, and that the `.title` rule is in `style.css`. The old class names are gone.
- **The times are not grey.** Check that the tag has `time`, and that the `.time` rule has `color: dimgray;`.
- **The times are not in typewriter letters.** Check the line `font-family: "Courier New", monospace;` in the `.time` rule, with a comma between the two names.
- **The page did not update.** Check that Go Live is running, and that every file is saved. A dot next to a file name in its tab means it is not saved.
