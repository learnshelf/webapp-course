# 3.6: A scale and a width

About 50 minutes.

By the end of this lesson every tag chooses its own spacing, from a short list of sizes, and your pages stop stretching across a wide window. You will meet your first **custom properties**, names for values that you write once. You will also take the gap out of `column`, `row` and `grid`, and write a width limit.

## The idea

Lesson 3.4 gave `column`, `row` and `grid` one gap, 1rem. It was the price of sharing them, and you saw it: the lines inside the club cards got looser. A tag cannot ask for a smaller gap. Space is a choice, and it should not be hidden inside the class that says where things go.

So the gap moves out. `column`, `row` and `grid` say only where the children go. A separate class says how far apart they are:

```
  before    <ul class="column">                 gap 1rem, always

  after     <ul class="column gap-md">          the same, by choice
            <li class="column gap-xs card">     a tighter one
```

Padding is the same kind of choice. In lesson 3.5 the padding went into the look, in `.card` and `.roomy`. A look class that sets padding fights with a padding class on the same tag, and the later rule wins. So the padding leaves the look too: `card` says how a card looks, and the tag says how much room is inside.

A page that has sizes of space in every rule is hard to keep even. So you pick a few sizes, a **scale**, and use only those. You write each size once, as a **custom property**: a name for a value.

```
  :root {
      --space-md: 1rem;               a name that starts with two hyphens, and its value
  }

  .gap-md {
      gap: var(--space-md);           var() uses the value
  }
```

`:root` means the whole page. A custom property that you write there is available in every rule. If you change the value, everything that uses it changes.

The second problem is on the Schedule page since lesson 3.2: on a wide window the rows stretch across the screen, and the name and the Delete button end up very far apart. A page needs a width limit, and the limited content needs to sit in the middle.

New words:

- **custom property**: a name for a value, written with two hyphens in front, such as `--space-md`. You use it with `var(--space-md)`.
- **scale**: a short list of sizes that you pick from, such as `xs`, `sm`, `md`, `lg` and `xl`.

## Steps

### 1. Start from last time

Open your project in VS Code and make sure Go Live is running. You will change all five files.

You should have `index.html`, `schedule.html`, `activities.html`, `layout.css` and `style.css`, as at the end of lesson 3.5.

Your homework may have changed your files. Take those changes out before you start, or keep a copy somewhere else, so your files match the end of the last lesson.

You should see: the three pages as at the end of lesson 3.5, with the first club on the Activities page in a red line.

### 2. The scale

At the very top of `layout.css`, above `.column`, add the sizes:

```css
:root {
    --space-xs: 0.25rem;
    --space-sm: 0.5rem;
    --space-md: 1rem;
    --space-lg: 1.5rem;
    --space-xl: 2rem;
}
```

A `rem` is the browser's text size, which is 16 pixels at the normal setting, as in lesson 1.4. So the five sizes are 4, 8, 16, 24 and 32 pixels.

Save and look at the browser.

You should see: nothing changed. The names exist, but no rule uses them yet.

### 3. Take the gap out

In `layout.css`, delete the `gap` line from `.column`, from `.row` and from `.grid`. They now look like this:

```css
.column {
    display: flex;
    flex-direction: column;
}

.row {
    display: flex;
}

.grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(14rem, 1fr));
}
```

Save and look at the Schedule and Activities pages.

You should see: everything touches. The rows of the Schedule have no space between them, the club cards are next to each other, and the two links in the top bar are next to each other, with no space between their boxes. The place classes no longer say how far apart things are.

### 4. The gap classes

Add three classes to the bottom of `layout.css`. The pages use three sizes of gap, so you write three classes:

```css
.gap-xs {
    gap: var(--space-xs);
}

.gap-sm {
    gap: var(--space-sm);
}

.gap-md {
    gap: var(--space-md);
}

```

`gap-md` is `gap: 1rem`, written as `var(--space-md)`. You write a class when a tag needs it. The scale has `lg` and `xl` as well, and no gap uses them yet, so there is no `gap-lg` or `gap-xl`. A class like this only works on a tag that is a flex container or a grid, because `gap` is the space between the children. That is what `row`, `column` and `grid` make.

Save and look at the browser.

You should see: nothing changed. No tag has a gap class yet.

### 5. Choose a gap for every tag

Give each tag the size it should have. Add the class right after `row`, `column` or `grid`:

```
  where                                         class to add

  schedule.html: the list, and each row         gap-md
  activities.html: the list of clubs            gap-md
  activities.html: each club card               gap-xs
  activities.html: the list of sessions         gap-md
  activities.html: each session                 gap-md
  both pages: the header (the top bar)          gap-md
  both pages: the nav (the two links)           gap-sm
  index.html: the main tag                      gap-md
```

For example, a row on the Schedule page and a club card become:

```html
<li class="row gap-md align-center card">
```

```html
<li class="column gap-xs card">
```

Change every tag in the list. Each club card gets `gap-xs`, and the two links in the top bar get `gap-sm`. If you like, VS Code can change the same text in every file at once: press Ctrl+Shift+H (Cmd+Shift+H on a Mac), type the old text and the new text, and look at the list before you replace.

Save and look at all three pages.

You should see: the pages as at the end of lesson 3.5, with two differences. The lines inside the club cards are close together again, 0.25rem apart as in lesson 3.3, and the two links in the top bar are closer, 0.5rem apart as in lesson 3.1. You can choose, and in lesson 3.4 you could not.

Now check that you did not miss a tag. Press Ctrl+Shift+F (Cmd+Shift+F on a Mac) to search in all your files. Search for `class="row"`, then for `class="column"`, then for `class="grid"`.

You should see: no results for any of them. A result is a tag that has `row`, `column` or `grid` and nothing else, so it still has no gap class. Then search for `gap-`. You should see `22 results in 4 files`: 19 in the three pages, one for each tag you changed, and 3 in `layout.css`. If the number is smaller, a tag that has other classes after `row` or `column`, such as `row align-center card`, still has no gap class.

### 6. Padding from the same scale

The pages have a rule `.page` that gives them room, with `padding: 1.5rem`. That is the size `lg`. Add a padding class for it to the bottom of `layout.css`:

```css
.padding-md {
    padding: var(--space-md);
}

.padding-lg {
    padding: var(--space-lg);
}

.padding-xl {
    padding: var(--space-xl);
}
```

In `schedule.html` and `activities.html`, change the opening `main` tag:

```html
<main class="padding-lg">
```

Delete the `.page` rule from `style.css`.

Save and look at the browser.

You should see: the same pages. `padding-lg` and `.page` said the same thing.

### 7. Padding on a card

The cards have padding too, in `.card`. Add two more padding classes to the bottom of `layout.css`, the sizes the cards will need:

```css
.padding-md {
    padding: var(--space-md);
}

.padding-xl {
    padding: var(--space-xl);
}
```

Try the new class on one card. In `schedule.html`, add `padding-xl` to the first row:

```html
<li class="row gap-md align-center padding-xl card">
```

Save and look at the browser.

You should see: nothing changed. The row keeps its 1rem of padding. `.card` and `.padding-xl` both set `padding`, and they are equally strong, so the later one wins, as in lesson 2.1. `style.css` comes after `layout.css` in the page, so `.card` wins. A look class that sets space takes the choice away from the tag.

So space leaves the look. Take `padding-xl` off the row. In `style.css`, delete the `padding: 1rem;` line from `.card`, and the `padding: 2rem;` line from `.roomy`. They now look like this:

```css
.card {
    background-color: white;
    border: 2px solid khaki;
    border-radius: 12px;
}

.roomy {
    margin: 1rem;
}
```

`.roomy` keeps the room around the front door, because the scale has no class for a margin. Now every card has no room inside, and each tag chooses its own. Press Ctrl+Shift+H (Cmd+Shift+H on a Mac) and replace `align-center card` with `align-center padding-md card`, and then `gap-xs card` with `gap-xs padding-md card`. Look at the list before you replace, and use it to see that you changed the rows and the club cards and nothing else. You can also change the tags by hand: put `padding-md` before `card` on each row, each club and each session. Then give the front door a bigger size, in `index.html`:

```html
<div class="padding-xl card roomy accent">
```

Save and look at all three pages.

You should see: the same pages as before this step. The rows and the club cards have 1rem inside, and the front door has 2rem. To check that no card was missed, search all your files for `padding-md`. You should see `12 results in 3 files`: 11 cards in the two pages, and the rule in `layout.css`.

A few rules in `style.css` keep their own numbers, such as the padding in `.btn`, `.tab` and `.app-bar`. They are the inside of one part, and no other tag needs to change them.

### 8. See the problem

Make the browser window wide, or zoom out with Ctrl and **-** (Cmd and **-** on a Mac), and look at the Schedule page.

You should see: the rows stretch across the whole window. The name is at one end and the Delete button at the other, far apart. Press Ctrl+0 (Cmd+0) when you are done.

### 9. A width limit

Add two classes to the bottom of `layout.css`:

```css
.width-lg {
    max-width: 48rem;
}

.center-self {
    margin-left: auto;
    margin-right: auto;
}
```

`max-width` means no wider than this. `width-lg` does not say how wide something is. It says how wide it may be. A tag that is narrower than its parent has room to spare, and `auto` as a margin takes that room, half on each side. So `center-self` puts the tag in the middle of its parent.

In `schedule.html` and `activities.html`, put both on `main`:

```html
<main class="padding-lg width-lg center-self">
```

Save and look at both pages with a wide window.

You should see: the content stays in a column that is 48rem wide, in the middle, with the yellow page on both sides. The top bar still goes across the whole window, because it is not in `main`. On a phone nothing changed, because a limit does not make anything narrower than it is. The `main` tag itself is 51rem wide, because the padding is outside the width, as in lesson 2.6. The content inside is 48rem. The name and the links in the top bar stay at the edges of the window, while the content is in the middle. That is fine for now.

### 10. Change one size

Open `layout.css` and change `--space-md` to `1.5rem`. Save and look at all three pages.

You should see: the rows, the cards, the lists and the front door all spaced out more, from one edit. Put it back to `1rem`.

### 11. Check your files

`layout.css`:

```css
:root {
    --space-xs: 0.25rem;
    --space-sm: 0.5rem;
    --space-md: 1rem;
    --space-lg: 1.5rem;
    --space-xl: 2rem;
}

.column {
    display: flex;
    flex-direction: column;
}

.row {
    display: flex;
}

.grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(14rem, 1fr));
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

.gap-xs {
    gap: var(--space-xs);
}

.gap-sm {
    gap: var(--space-sm);
}

.gap-md {
    gap: var(--space-md);
}

.padding-lg {
    padding: var(--space-lg);
}

.padding-md {
    padding: var(--space-md);
}

.padding-xl {
    padding: var(--space-xl);
}

.width-lg {
    max-width: 48rem;
}

.center-self {
    margin-left: auto;
    margin-right: auto;
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
    <header class="row gap-md justify-between align-center app-bar">
        <a class="app-name" href="index.html">Student Planner</a>
        <nav class="row gap-sm">
            <a class="tab current" href="schedule.html">Schedule</a>
            <a class="tab" href="activities.html">Activities</a>
        </nav>
    </header>
    <main class="padding-lg width-lg center-self">
        <h1>My Schedule</h1>
        <p class="muted">4 lessons, the same every day</p>
        <ul class="column gap-md">
            <li class="row gap-md align-center padding-md card">
                <span class="width-fill title">Mathematics</span>
                <span class="time">08:30-09:20</span>
                <button class="btn">Delete</button>
            </li>
            <li class="row gap-md align-center padding-md card">
                <span class="width-fill title">English</span>
                <span class="time">09:30-10:20</span>
                <button class="btn">Delete</button>
            </li>
            <li class="row gap-md align-center padding-md card">
                <span class="width-fill title">Biology</span>
                <span class="time">10:40-11:30</span>
                <button class="btn">Delete</button>
            </li>
            <li class="row gap-md align-center padding-md card">
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
    <header class="row gap-md justify-between align-center app-bar">
        <a class="app-name" href="index.html">Student Planner</a>
        <nav class="row gap-sm">
            <a class="tab" href="schedule.html">Schedule</a>
            <a class="tab current" href="activities.html">Activities</a>
        </nav>
    </header>
    <main class="padding-lg width-lg center-self">
        <h1>Activities</h1>
        <h2>Clubs</h2>
        <ul class="grid gap-md">
            <li class="column gap-xs padding-md card accent">
                <span class="title">Chess club</span>
                <span class="muted">Mondays and Thursdays</span>
                <span class="muted">15:30-16:30</span>
            </li>
            <li class="column gap-xs padding-md card">
                <span class="title">Drama club</span>
                <span class="muted">Tuesdays</span>
                <span class="muted">16:00-17:30</span>
            </li>
            <li class="column gap-xs padding-md card">
                <span class="title">Robotics</span>
                <span class="muted">Wednesdays</span>
                <span class="muted">15:30-17:00</span>
            </li>
        </ul>
        <h2>Coming up</h2>
        <ul class="column gap-md">
            <li class="row gap-md align-center padding-md card">
                <span class="session-day">Mon 9 Nov</span>
                <span class="width-fill session-name">Chess club</span>
                <span class="time">15:30</span>
            </li>
            <li class="row gap-md align-center padding-md card">
                <span class="session-day">Tue 10 Nov</span>
                <span class="width-fill session-name">Drama club</span>
                <span class="time">16:00</span>
            </li>
            <li class="row gap-md align-center padding-md card">
                <span class="session-day">Wed 11 Nov</span>
                <span class="width-fill session-name">Robotics</span>
                <span class="time">15:30</span>
            </li>
            <li class="row gap-md align-center padding-md card">
                <span class="session-day">Thu 12 Nov</span>
                <span class="width-fill session-name">Chess club</span>
                <span class="time">15:30</span>
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
    <main class="column gap-md align-center justify-center landing">
        <div class="padding-xl card roomy accent">
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
    border: 2px solid khaki;
    border-radius: 12px;
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

### 12. Save it

Save your work with the routine, and push it. The caption is `3.6 A scale and a width`. The [git cheatsheet](../reference/01-git-cheatsheet.md) has the commands.

## Recap

- A custom property is a name for a value: `--space-md: 1rem;`. You use it with `var(--space-md)`. Write it in `:root` and every rule can use it.
- A scale is a short list of sizes. Using only those keeps a page even, and you change a size in one place.
- Space is a choice, so it has its own classes, from the scale: `gap-xs`, `gap-sm` and `gap-md`, and `padding-md`, `padding-lg` and `padding-xl`. You write a class when a tag needs it. `column`, `row` and `grid` say only where the children go, and `card` says only how a card looks.
- A look class should not set space. `.card` set `padding`, so it beat `padding-xl` on the same tag, because it comes later in the page. The padding moved out of `.card`, and each tag chooses it.
- A `gap` class needs a tag that is a flex container or a grid.
- `max-width` limits how wide a tag may be. It does not make anything wider or narrower than it is.
- `margin-left: auto` and `margin-right: auto` put a tag that is narrower than its parent in the middle.
- Your layout classes are `column`, `row`, `grid`, `justify-between`, `justify-center`, `align-center`, `width-fill`, the gap classes, the padding classes, `width-lg` and `center-self`. They are fifteen classes, and you wrote them all.

## Homework

Each should take about five minutes.

1. **One card different.** Give the Drama club the class `gap-sm` in place of `gap-xs`. You know it worked when only that card has more space between its lines, and you wrote no rule. On a wide window the cards in a row are the same height, so the other two cards may have empty space at the bottom. Put `gap-xs` back when you are done.

2. **Predict, then check.** Before you try each one, say what you will see on a wide window. Then put it on the `main` of `schedule.html`, look, and put it back.

   ```
   a   <main class="width-lg center-self">
   b   <main class="padding-lg width-lg">
   c   <main class="padding-lg center-self">
   ```

   You know it worked when you got at least two right, and you can say why (c) changes nothing, and what (a) does on a narrow window. Hint: `auto` takes the room that is left, and a block fills its parent.

3. **A bigger size.** Add a size to the scale, `--space-2xl: 3rem;`, and a class `.gap-2xl` that uses it. Put it on the `main` of the front door in `index.html`, in place of `gap-md`. You know it worked when the card and the line "Made by Sam" are further apart, and you can say which two places you changed in `layout.css`. Take `--space-2xl` and `.gap-2xl` out of `layout.css`, and put `gap-md` back on the `main`, when you are done.

4. **Stretch: more room for one card.** Put `padding-xl` in place of `padding-md` on the Chess club card, the first one. You know it worked when only that card has more room inside, and you wrote no rule. In step 7 the same class did nothing, and you can say why it works now. Put `padding-md` back when you are done.

## Stuck?

- **Everything touches.** The tags need a gap class, such as `gap-md`. Check that each `row`, `column` and `grid` has one, and that the name is spelled the same in `layout.css`. The search at the end of step 5 finds the tags that were missed.
- **A gap class does nothing.** The tag needs `row`, `column` or `grid` as well. They make it a container.
- **A size does not work.** Check that the name has two hyphens, `--space-md`, and the same name in `var(--space-md)`. Check the colon and the semicolon in `:root`. A missing semicolon can break the size on the next line too.
- **The page is not in the middle.** `main` needs both `width-lg` and `center-self`. One of them alone does not centre it.
- **A padding class does nothing.** Check that no other class on the tag sets `padding`. In `style.css`, `.card` and `.roomy` must not have a `padding` line.
- **The cards have no room inside.** Every tag with `card` needs `padding-md`. Search all your files for `padding-md`: you should see `12 results in 3 files`.
- **The page has no room around it.** Check that `main` has `padding-lg`, and that `layout.css` has the `.padding-lg` rule.
- **The page did not update.** Check that Go Live is running, and that every file is saved. A dot next to a file name in its tab means it is not saved.
