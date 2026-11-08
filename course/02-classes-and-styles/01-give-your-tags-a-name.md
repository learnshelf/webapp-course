# 2.1: Give your tags a name

About 30 minutes.

By the end of this lesson your front door will have a blue button, an italic tagline and a small grey note at the bottom. You will write your first **classes**: names you give to tags, so that a CSS rule can style some tags of a kind and leave the others alone.

## The idea

So far every rule you wrote was about a kind of tag: `body`, `h1`, `p`. A rule for `p` styles every paragraph on the page. That is too blunt when you want just one paragraph to look different.

A **class** is a name you choose. Using one takes two steps:

```
  1. in the HTML, give the tag the name         <p class="tagline">
  2. in the CSS, write a rule for the name      .tagline { font-style: italic; }
                                                (the dot means "class")
```

The name has to match in both places. The dot is only in the CSS.

Four things to know:

```
  one class on many tags      class="muted" can go on a p, a button, any tag
  many classes on one tag     class="tagline muted", names separated by a space
  a class beats a tag rule    .muted { font-size: 1rem }  wins over  p { font-size: 1.5rem }
  two classes disagree        the one lower in the file wins
```

Pick names that explain themselves, in lowercase, with no spaces. Use a hyphen between words, like `main-title`.

New words:

- **class**: a name you give to a tag.
- **class selector**: a CSS rule for a class, written with a dot: `.tagline`.
- **padding**: the space inside a tag, between its words and its edge.
- **border-radius**: how round the corners are.

## Steps

### 1. Start from last time

Open your project in VS Code and make sure Go Live is running.

Your homework may have changed your files. Take those changes out before you start, or keep a copy somewhere else, so your files match the listing below.

`index.html` should have this inside the `body`:

```html
<body>
    <main>
        <h1>Student Planner</h1>
        <p>Welcome, Sam</p>
        <button>Continue</button>
    </main>
</body>
```

`style.css` should look like this. Your colours and font may be different, and that is fine:

```css
body {
    background-color: lightyellow;
    text-align: center;
    color: darkslategray;
    font-family: Georgia, serif;
}

h1 {
    font-size: 3rem;
    color: firebrick;
}

p {
    font-size: 1.5rem;
}
```

### 2. Add two more lines

In `index.html`, add a tagline under the welcome line, and a note under the button. Use your own first name:

```html
<main>
    <h1>Student Planner</h1>
    <p>Welcome, Sam</p>
    <p>Plan your week</p>
    <button>Continue</button>
    <p>Made by Sam</p>
</main>
```

Save and look at the browser.

You should see: two new lines, one under the welcome line and one under the button. They look just like the welcome line, because the `p` rule styles every paragraph.

### 3. See why a tag rule is too blunt

You want the tagline and the note to look quieter than the welcome line. Try it the way you know. Add a colour to the `p` rule:

```css
p {
    font-size: 1.5rem;
    color: dimgray;
}
```

Save and look at the browser.

You should see: all three lines turn grey, the welcome line too. A rule for `p` cannot tell your paragraphs apart.

Take the `color: dimgray;` line out again. Save.

### 4. Make your first class

Give the tagline a name. In `index.html`, add `class="tagline"` to its opening tag:

```html
<p class="tagline">Plan your week</p>
```

Save and look at the browser.

You should see: nothing changed. A name by itself does nothing, just like the `main` tag in lesson 1.2.

Now write the rule for the name. `font-style: italic` makes the letters lean. Add this at the bottom of `style.css`:

```css
.tagline {
    font-style: italic;
}
```

Save and look at the browser.

You should see: only the tagline is in italics. The welcome line and the note are not. The rule is for `.tagline`, so it only reaches the tag with that name.

### 5. Use one class on more than one tag

Some looks belong on several tags. Write a second class, under the first:

```css
.muted {
    color: dimgray;
    font-size: 1rem;
}
```

Give the note that name:

```html
<p class="muted">Made by Sam</p>
```

Save and look at the browser.

You should see: the note turns grey and gets smaller than the welcome line. The rule for `p` says `1.5rem` and the rule for `.muted` says `1rem`. They disagree, and the class wins. You will see more of that in step 7.

Now give the tagline the same name, as a second class. A tag can have several, separated by a space:

```html
<p class="tagline muted">Plan your week</p>
```

Save and look at the browser.

You should see: the tagline is italic, grey and small. It gets the looks of both classes.

The grey is written once, and two tags use it. Change `dimgray` to `firebrick` in the `.muted` rule, save, and both lines change. Then change it back.

### 6. Style the button with a class

Give the button a class too. `btn` is short for button:

```html
<button class="btn">Continue</button>
```

Write the rule for it at the bottom of `style.css`:

```css
.btn {
    background-color: #2350c8;
    color: white;
    border: none;
    border-radius: 6px;
    padding: 0.6rem 1.2rem;
    font-size: 1rem;
    cursor: pointer;
}
```

- `#2350c8` is a colour written as a code: a `#` and six letters and digits. The [CSS cheatsheet](../reference/03-css-cheatsheet.md) lists the other ways to write a colour.
- `border: none` takes away the browser's edge around the button.
- `border-radius` rounds the corners.
- `padding` is the space between the words and the edge of the button. `0.6rem 1.2rem` has two values: the first is the space above and below the words, and the second is the space at the left and right. You will meet it properly in [lesson 2.6](06-the-box.md).
- `cursor: pointer` shows a hand when the mouse is over the button.

Save and look at the browser.

You should see: a blue button with white words and rounded corners. Move the mouse over it and the pointer turns into a hand. It still does nothing when you click it. It gets its job in a later lesson.

Why a class, and not a rule for `button`? Your app will have other buttons, such as Add and Delete, and they will not all look the same. A class lets you choose which buttons get this look.

### 7. A class beats a tag, whatever the order

Look at your file. The `p` rule comes first and the `.muted` rule comes after it. Move the whole `.muted` rule above the `p` rule, and save.

You should see: nothing changes. The note is still small and grey.

When a class and a tag disagree, the class wins, wherever it is in the file. CSS ranks the kinds of selector, and a class ranks above a tag name. How many tags carry the class makes no difference: a class on every `p` on the page still beats the `p` rule.

Move the `.muted` rule back, directly under the `p` rule and above `.tagline`.

### 8. Two classes that disagree

A class beats a tag. But what if two classes disagree? Add a new class at the bottom of `style.css`:

```css
.warm {
    color: firebrick;
}
```

Give the note both classes:

```html
<p class="muted warm">Made by Sam</p>
```

Save and look at the browser.

You should see: the note is red. `.muted` says `dimgray` and `.warm` says `firebrick`. Both are classes, so neither one is stronger. The one lower in the file wins, and `.warm` is lower.

Now move the whole `.warm` rule above the `.muted` rule, and save.

You should see: the note is grey again. Now `.muted` is lower, so `.muted` wins.

One more try. Write the names the other way round, `class="warm muted"`, and save.

You should see: nothing changes. The order of the names inside `class="..."` does not matter. The order of the rules in `style.css` does.

Take the experiment away. Delete the `.warm` rule from `style.css`, and change the tag back to `class="muted"`. Save.

You should see: the small grey note, as before.

### 9. Check your files

`index.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Student Planner</title>
    <link rel="stylesheet" href="style.css">
    <link rel="icon" type="image/svg+xml" href="favicon.svg">
</head>
<body>
    <main>
        <h1>Student Planner</h1>
        <p>Welcome, Sam</p>
        <p class="tagline muted">Plan your week</p>
        <button class="btn">Continue</button>
        <p class="muted">Made by Sam</p>
    </main>
</body>
</html>
```

`style.css`:

```css
body {
    background-color: lightyellow;
    text-align: center;
    color: darkslategray;
    font-family: Georgia, serif;
}

h1 {
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
}

.btn {
    background-color: #2350c8;
    color: white;
    border: none;
    border-radius: 6px;
    padding: 0.6rem 1.2rem;
    font-size: 1rem;
    cursor: pointer;
}
```

### 10. Save it

Save your work with the routine, and push it. The caption is `2.1 Give your tags a name`. The [git cheatsheet](../reference/01-git-cheatsheet.md) has the commands.

## Recap

- A rule for a tag, like `p`, styles every tag of that kind.
- A class is a name you give to a tag: `class="tagline"`. The CSS rule for it starts with a dot: `.tagline`.
- The name must match in the HTML and the CSS. The dot is only in the CSS.
- One class can go on many tags, so a look is written once and used many times.
- One tag can have several classes, separated by a space: `class="tagline muted"`.
- When a class and a tag rule disagree, the class wins, wherever it is in the file.
- When two classes disagree, neither is stronger, and the one lower in `style.css` wins. The order of the names in `class="..."` does not matter.

## Homework

Each should take about five minutes.

1. **Your own button.** Change the `.btn` rule to suit you: the colours, `border-radius` (try `0`, `6px` and `30px`) and `padding`. Keep the words easy to read. You know it worked when the button looks like yours, and the other lines did not change. Before the next lesson, put the `.btn` rule back as it is in step 6.

2. **Use a class again.** Add one more line to the page, such as today's date, and give it `class="muted"`. Then change the colour in the `.muted` rule once. You know it worked when you changed one rule and every muted line changed with it. Take the date line out again when you are done, and put the colour back to `dimgray`.

3. **Stretch: a second button.** Add a second button, `<button class="btn quiet">Look around</button>`. Write a `.quiet` rule with `background-color: transparent;` and `color: #2350c8;`, under the `.btn` rule. You know it worked when the second button shows blue words without the blue box, and the Continue button is unchanged. If the second button stays blue, move `.quiet` below `.btn`. Two classes of the same strength disagree, and the one lower in the file wins. Take the second button and the `.quiet` rule out again when you are done. (Lesson 2.4 has a task that uses them, so you can put them back then.)

## Stuck?

- **A class does nothing.** Check that the name is spelled the same in both files. In `index.html` it is `class="tagline"`, with no dot. In `style.css` it is `.tagline`, with a dot. Check the quotes, the curly brackets `{ }` and the semicolons `;`.
- **Only one of two classes works.** Both names go inside one `class="..."`, separated by a space. If you write `class="tagline" class="muted"`, the browser reads only the first.
- **The note stays grey after I add `.warm`.** The `.warm` rule has to be below the `.muted` rule in `style.css`, and the tag has to say `class="muted warm"`. When two classes disagree, the one lower in the file wins.
- **The second button stays blue.** The `.quiet` rule has to come below the `.btn` rule. When two classes disagree, the later one wins.
- **The button looks plain.** Check that the button tag says `class="btn"` and that the rule in `style.css` is `.btn`.
- **You cannot read the words on the button.** The text and the background are too close in colour. Make one of them lighter or darker.
- **The note is not smaller.** Check that the tag says `class="muted"` and that the `.muted` rule has `font-size: 1rem;`.
- **The page did not update.** Check that Go Live is running and both files are saved. A dot next to a file name in its tab means it is not saved.
