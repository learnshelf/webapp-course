# 3.4: The same thing twice

About 50 minutes.

By the end of this lesson the lines that say where things go have moved out of your classes into one small file, `layout.css`. All three of your pages use it, and they look the same as before, with a little difference in the space. You will name classes for the arrangement and not for the content, and put several on one tag.

## The idea

In the last two lessons you wrote a class for every part, named for what it holds: `courses`, `course`, `activities`, `activity`, `upcoming`, `session`. Each of them does two jobs. It says where its children go, and, for some, how the box looks. Sort the lines of each rule into those two jobs, and look at the first one:

```
  rule          where the children go                       how it looks

  .courses      a column, gap 0.75rem                       -
  .upcoming     a column, gap 0.75rem                       -
  .activity     a column, gap 0.25rem                       a white box with a line
  .course       a row, centred up and down, gap 1rem        a white box with a line
  .session      a row, centred up and down, gap 1rem        a white box with a line
  .tabs         a row, gap 0.5rem                           -
  .app-bar      a row, the ends apart, centred up and down  a white bar with a line
  .activities   a grid, as many columns as fit, gap 1rem    -
```

Eight names, but only four arrangements: a column, a row, a row with the ends apart, and a grid. `courses`, `upcoming` and `activity` all do the same: they stack their children. The names do not show it, because they describe what is inside, not what the class does.

That is how most people name classes. It feels natural, because the list of courses is `courses`. The cost is that every new list needs a new class with the same lines, and a class like `.course` cannot be used for anything that is not a course.

The way out is to split the two jobs. A class that says only where the children go is a **place class**. You name it for the arrangement: `column`, `row`, `grid`. It can go on any tag, whatever is inside. What is left in your own classes is how things look. That is lesson 3.5.

A tag can have several classes, so a tag gets the arrangement it needs and the look it needs:

```
  <li class="row align-center course">
        |    |            |
        |    |            +-- how it looks (for now, still your own class)
        +----+--------------- where its children go
```

New words:

- **place class**: a class that says only where the children of a tag go, such as `column`.

## Steps

### 1. Start from last time

Open your project in VS Code and make sure Go Live is running. You will make a new file, and change all the others.

You should have `index.html`, `schedule.html`, `activities.html` and `style.css`. The Schedule and Activities pages have their lists, and the top bar.

Your homework may have changed your files. Take those changes out before you start, or keep a copy somewhere else, so your files match the end of the last lesson.

You should see: the Schedule page with four rows, and the Activities page with three cards and four sessions.

### 2. A file for the arrangements

Make a new file called `layout.css`, next to the others:

```css
.column {
    display: flex;
    flex-direction: column;
    gap: 1rem;
}

.row {
    display: flex;
    gap: 1rem;
}

.grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(14rem, 1fr));
    gap: 1rem;
}

.justify-between {
    justify-content: space-between;
}

.align-center {
    align-items: center;
}

.width-fill {
    flex: 1;
}
```

Every line is one you have already written. The names say what the class does:

- `column` and `row` make a flex container with a direction. They use one gap, 1rem.
- `grid` makes a grid with as many columns as fit.
- `justify-between` is `justify-content: space-between`, and `align-center` is `align-items: center`. These two depend on the direction, as in lesson 2.5. In a row, `align-center` centres up and down. In a column it centres left and right. Use them on a `row` or a `column`. On a `grid` whose columns are `1fr`, `justify-between` and `justify-center` do nothing, because the columns already fill the width.
- `width-fill` is `flex: 1`: this child takes the space that is left. It is for a child in a row. In a column it shares the height that is left, and that only matters when the column has a height.

None of them has a colour, a border or a size for text. They say only where things go.

### 3. Use the file on the pages

In `schedule.html` and in `activities.html`, add a line to the `head`, above the line for `style.css`:

```html
<link rel="stylesheet" href="layout.css">
<link rel="stylesheet" href="style.css">
```

`layout.css` goes first. When two rules disagree, the one that comes later wins, as in lesson 2.1, so your looks in `style.css` have the last word.

Save and look at the browser.

You should see: nothing changed. The file is there, but no tag uses its classes yet.

### 4. The Schedule page

In `schedule.html`, give the list, each row and each name their new classes. Here is the first row:

```html
<ul class="column">
    <li class="row align-center course">
        <span class="width-fill course-name">Mathematics</span>
        <span class="course-time">08:30-09:20</span>
        <button class="btn">Delete</button>
    </li>
```

`courses` is gone, and `column` takes its place. The row keeps `course`, which still gives the look, and gets `row` and `align-center` in front of it. Change all four items the same way.

Save and look at the browser.

You should see: almost the same page. The space between the rows is a little bigger, because `column` has a gap of 1rem and `.courses` had 0.75rem. The old rules are still in `style.css`, and they stay there until step 7. The `.course` and `.course-name` rules say the same thing as the new classes, so you cannot see them. The `.courses` rule has no tag left to style.

### 5. The Activities page

In `activities.html`, change the list of clubs, each club, the list of sessions, each session and the name of each session. Here are the first club and the first session:

```html
<ul class="grid">
    <li class="column activity">
        <span class="activity-name">Chess club</span>
        <span class="activity-days muted">Mondays and Thursdays</span>
        <span class="activity-time muted">15:30-16:30</span>
    </li>
```

```html
<ul class="column">
    <li class="row align-center session">
        <span class="session-day">Mon 9 Nov</span>
        <span class="width-fill session-name">Chess club</span>
        <span class="session-time">15:30</span>
    </li>
```

`activities` became `grid`, `upcoming` became `column`, and the cards and the rows got the classes that say where their children go. The sessions are a column, like the list of rows on the Schedule page, and they use the same class. Change all of them.

Save and look at the browser.

You should see: the same page. The sessions are a little further apart.

### 6. The top bar

The top bar is in both pages. In each file, change the `header` and the `nav`:

```html
<header class="row justify-between align-center app-bar">
    <a class="app-name" href="index.html">Student Planner</a>
    <nav class="row">
```

The tabs were `tabs`, and now they are a `row`.

Save and look at the browser, and click between the two pages.

You should see: the same bar. The two links are a little further apart, because `row` has a gap of 1rem and `.tabs` had 0.5rem.

### 7. Take the arranging lines out of style.css

Now `style.css` has lines that do nothing, because `layout.css` already says them. Delete these four rules completely, with their curly brackets:

```
  .courses     .upcoming     .activities     .tabs
```

Then, in each of these six rules, delete the lines that say where the children go, and keep the ones that say how it looks. The `width` in `.session-day` stays, because it is about how wide the day is, and not about where children go:

```
  .app-bar        delete display, justify-content, align-items
  .course         delete display, align-items, gap
  .course-name    delete flex
  .activity       delete display, flex-direction, gap
  .session        delete display, align-items, gap
  .session-name   delete flex
```

The six rules should now look like this:

```css
.app-bar {
    padding: 0.75rem 1.5rem;
    background-color: white;
    border-bottom: 2px solid khaki;
}

.course {
    padding: 1rem;
    background-color: white;
    border: 2px solid khaki;
    border-radius: 8px;
}

.course-name {
    font-size: 1.1rem;
    font-weight: bold;
}

.activity {
    padding: 1rem;
    background-color: white;
    border: 2px solid khaki;
    border-radius: 8px;
}

.session {
    padding: 1rem;
    background-color: white;
    border: 2px solid khaki;
    border-radius: 8px;
}

.session-name {
    font-size: 1.1rem;
}
```

Save and look at the browser.

You should see: the Schedule page and the top bar as in step 6. The club cards are a little looser inside, because `column` has a gap of 1rem and `.activity` had 0.25rem. Nothing else changed. One gap for everything is the price of a shared class. Lesson 3.6 gives you the choice back, with a separate class for the size.

### 8. Count again

Press Ctrl+F (Cmd+F on a Mac) in `style.css`, and search for `display: flex`.

You should see: one result, in the `.landing` rule. It was 8 at the end of lesson 3.3. Step 9 takes care of the last one. Search in `layout.css`: two. Close the search with Escape.

### 9. The front door

The front door is arranged by `.landing`, with five lines. It is a column, centred both ways. Use the same classes.

In `index.html`, add the link to `layout.css` above the link to `style.css`, and change the opening `main` tag:

```html
<link rel="stylesheet" href="layout.css">
<link rel="stylesheet" href="style.css">
```

```html
<main class="column align-center justify-center landing">
```

`layout.css` needs one more class. Add it under `.justify-between`:

```css
.justify-center {
    justify-content: center;
}
```

In `style.css`, change the `.landing` rule so it keeps only what is not an arrangement:

```css
.landing {
    min-height: 100vh;
    text-align: center;
}
```

Save, open `index.html` in the browser and look.

You should see: exactly the same front door, in the middle of the window, both ways. The five lines of lesson 2.5 are now three words: `column align-center justify-center`. Search for `display: flex` in `style.css` once more: no results. Every flex container in the app now comes from two rules, `.column` and `.row`.

### 10. Check your files

`layout.css`:

```css
.column {
    display: flex;
    flex-direction: column;
    gap: 1rem;
}

.row {
    display: flex;
    gap: 1rem;
}

.grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(14rem, 1fr));
    gap: 1rem;
}

.justify-between {
    justify-content: space-between;
}

.justify-center {
    justify-content: center;
}

.align-center {
    align-items: center;
}

.width-fill {
    flex: 1;
}
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
            <li class="row align-center course">
                <span class="width-fill course-name">Mathematics</span>
                <span class="course-time">08:30-09:20</span>
                <button class="btn">Delete</button>
            </li>
            <li class="row align-center course">
                <span class="width-fill course-name">English</span>
                <span class="course-time">09:30-10:20</span>
                <button class="btn">Delete</button>
            </li>
            <li class="row align-center course">
                <span class="width-fill course-name">Biology</span>
                <span class="course-time">10:40-11:30</span>
                <button class="btn">Delete</button>
            </li>
            <li class="row align-center course">
                <span class="width-fill course-name">History</span>
                <span class="course-time">11:40-12:30</span>
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
            <li class="column activity">
                <span class="activity-name">Chess club</span>
                <span class="activity-days muted">Mondays and Thursdays</span>
                <span class="activity-time muted">15:30-16:30</span>
            </li>
            <li class="column activity">
                <span class="activity-name">Drama club</span>
                <span class="activity-days muted">Tuesdays</span>
                <span class="activity-time muted">16:00-17:30</span>
            </li>
            <li class="column activity">
                <span class="activity-name">Robotics</span>
                <span class="activity-days muted">Wednesdays</span>
                <span class="activity-time muted">15:30-17:00</span>
            </li>
        </ul>
        <h2>Coming up</h2>
        <ul class="column">
            <li class="row align-center session">
                <span class="session-day">Mon 9 Nov</span>
                <span class="width-fill session-name">Chess club</span>
                <span class="session-time">15:30</span>
            </li>
            <li class="row align-center session">
                <span class="session-day">Tue 10 Nov</span>
                <span class="width-fill session-name">Drama club</span>
                <span class="session-time">16:00</span>
            </li>
            <li class="row align-center session">
                <span class="session-day">Wed 11 Nov</span>
                <span class="width-fill session-name">Robotics</span>
                <span class="session-time">15:30</span>
            </li>
            <li class="row align-center session">
                <span class="session-day">Thu 12 Nov</span>
                <span class="width-fill session-name">Chess club</span>
                <span class="session-time">15:30</span>
            </li>
        </ul>
    </main>
</body>
</html>
```

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
        <div class="card">
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
    background-color: white;
    padding: 2rem;
    border: 2px solid firebrick;
    border-radius: 12px;
    margin: 1rem;
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

.course {
    padding: 1rem;
    background-color: white;
    border: 2px solid khaki;
    border-radius: 8px;
}

.course-name {
    font-size: 1.1rem;
    font-weight: bold;
}

.course-time {
    color: dimgray;
    font-family: "Courier New", monospace;
}

.activity {
    padding: 1rem;
    background-color: white;
    border: 2px solid khaki;
    border-radius: 8px;
}

.activity-name {
    font-size: 1.1rem;
    font-weight: bold;
}

.session {
    padding: 1rem;
    background-color: white;
    border: 2px solid khaki;
    border-radius: 8px;
}

.session-day {
    width: 7rem;
    font-weight: bold;
}

.session-name {
    font-size: 1.1rem;
}

.session-time {
    color: dimgray;
    font-family: "Courier New", monospace;
}
```

### 11. Save it

Save your work with the routine, and push it. The caption is `3.4 The same thing twice`. The [git cheatsheet](../reference/01-git-cheatsheet.md) has the commands.

## Recap

- Names taken from the content, such as `courses` and `activities`, hide that different things are arranged in the same way.
- A place class says only where the children of a tag go, and it is named for the arrangement: `column`, `row`, `grid`. It can go on any tag.
- A tag can have several classes: `row align-center course`. The place classes arrange it, and the look class styles it.
- `align-center` and `justify-between` are `align-items` and `justify-content`, so they follow the direction: in a row, `align-center` is up and down, and in a column, left and right.
- `layout.css` goes before `style.css`, so a look can overrule an arrangement if it has to.
- A change to a place class changes every tag that uses it, in all the pages. Before, it was a change to every rule that copied the lines.
- What is left in `style.css` is how things look. Lesson 3.5 turns that into classes you can reuse.

## Homework

Each should take about five minutes.

1. **One edit.** In `layout.css`, change the `gap` in `.column` to `2rem`. Look at all three pages. You know it worked when every list, the inside of every club card and the front door changed together, and you edited one line. Before this lesson the gaps were in four rules, `.courses`, `.upcoming`, `.activity` and `.landing`, and they had three different sizes. Then put the gap back to `1rem`.

2. **Predict, then check.** Before you try each one, say where the name, the time and the button will go. Then do it to the first row on the Schedule page, look, and put it back.

   ```
   a   <li class="column align-center course">
   b   <li class="column course">
   ```

   You know it worked when you got both right, and you can say why `align-center` moved things left and right here, and up and down in the row. Hint: lesson 2.5. In (b) a child that has no `align-center` stretches across the container.

3. **An arrangement for free.** In `activities.html`, change the list of sessions from `class="column"` to `class="grid"`. You know it worked when the sessions are in columns that re-flow when the window changes, and you wrote no CSS. The rows get cramped in a narrow window. That is the cost of this arrangement for this content. Put it back when you are done.

4. **Stretch: a class that wraps.** Add one more class to `layout.css`: `.wrap { flex-wrap: wrap; }`. Add `wrap` to the rows of the Schedule page: `<li class="row align-center wrap course">`. Open the phone view as in lesson 3.1. You know it worked when you can say what `wrap` did to the Delete button in the rows, and why it did not change the rows on a wide window. Take `wrap` out of the rows, and the `.wrap` rule out of `layout.css`, when you are done.

## Stuck?

- **The page lost its arrangement.** Check that the `head` has `<link rel="stylesheet" href="layout.css">`, spelled the same as the file, and that the file is in the same folder.
- **A class does nothing.** Check that the name in `class="..."` and the name in `layout.css` are spelled the same, and that the rule has the dot: `.column`.
- **`align-center` does nothing.** It needs `row` or `column` on the same tag. They make the flex container.
- **The looks are gone.** You deleted too many lines in step 7. Delete only the lines that say where the children go, and keep `padding`, `background-color`, `border`, `border-radius`, `font-size` and `font-weight`.
- **Most of the page lost its style after step 7.** Check the curly brackets in `style.css`. Every rule ends with `}`, and a rule you delete must go completely, from its name to its `}`. A `}` left behind, or one that you deleted by mistake, can spoil every rule under it. Search `style.css` for `{`, then for `}`: the two numbers should be the same.
- **The front door is not in the middle.** Check that the `main` tag has `column align-center justify-center landing`, that `index.html` has the link to `layout.css`, and that `.justify-center` is in `layout.css`.
- **The page did not update.** Check that Go Live is running, and that every file is saved. A dot next to a file name in its tab means it is not saved.
