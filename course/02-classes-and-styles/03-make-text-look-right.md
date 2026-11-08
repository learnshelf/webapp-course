# 2.3: Make text look right

About 20 minutes.

By the end of this lesson your page will have more room between its lines, a tagline in spaced-out capital letters and a bold button label. You will know five properties that change how text looks, and whether each one belongs on `body` or on a class.

## The idea

So far you changed text with `color`, `font-family`, `font-size` and `font-style`. CSS has many more properties for text. Today you meet five:

```
  line-height       the height of each line, as a multiple of the text size
  letter-spacing    the space between letters
  text-transform    capitals or lower case, without touching the HTML
  font-weight       how heavy the letters are: normal or bold
  text-decoration   a line through, under or over the text
```

There is nothing new to learn about how to write them. Each one is a property and a value in a rule, like the ones you already write. The new part is choosing where each one goes. Put it on `body` when you want every line to have it, because it flows down, as you saw in lesson 1.4. Put it on a class when you want only some tags to have it.

New words:

- **line-height**: the height of one line of text. `1.5` means one and a half times the text size.
- **letter-spacing**: the space between the letters.
- **text-transform**: changes the capital letters on the screen, not in your HTML.
- **font-weight**: how heavy the letters are.
- **text-decoration**: a line through, under or over the text.

## Steps

### 1. Start from last time

Open your project in VS Code and make sure Go Live is running. You will only change `style.css` today.

Your homework may have changed your files. Take those changes out before you start, or keep a copy somewhere else, so your files match the listing below.

`index.html` should have this inside the `body`:

```html
<body>
    <main>
        <h1>Student Planner</h1>
        <p>Welcome, Sam</p>
        <p class="tagline muted">Plan your week</p>
        <button class="btn">Continue</button>
        <p class="muted">Made by Sam</p>
    </main>
</body>
```

`style.css` should look like the end of lesson 2.1. Your colours and font may be different, and that is fine.

### 2. More room between the lines

Add `line-height` to the `body` rule:

```css
body {
    background-color: lightyellow;
    text-align: center;
    color: darkslategray;
    font-family: Georgia, serif;
    line-height: 1.5;
}
```

Save and look at the browser.

You should see: the lines move a little further apart. Every line is taller, so there is more space above and below each one. You set it on `body`, so most of the tags inside got it. The button is the exception. The browser gives a button its own font and line height, and it keeps them until you ask for something else. The line `font-family: inherit;` in the `.btn` rule would make the button use the font of the page.

The number has no unit. It means a multiple of the text size, so big text gets big lines and small text gets small lines. Try `1`, then `2.5`, and then put it back to `1.5`.

The space between lines shows best when a line wraps. Make your browser window narrow, until the title breaks onto two lines, and look at the gap between the two. Or press Ctrl and + (Cmd and + on a Mac) a few times to zoom in, which has the same effect. Then make the window wide again, or press Ctrl and 0 (Cmd and 0) to zoom back.

### 3. Spread out the letters

Add `letter-spacing` to the `.tagline` rule:

```css
.tagline {
    font-style: italic;
    letter-spacing: 0.15rem;
}
```

Save and look at the browser.

You should see: the letters of the tagline are further apart. The other lines did not change, because the rule is only for `.tagline`.

Try `0.5rem`. Then try `-0.05rem`, with a minus sign, and look at the letters. Put it back to `0.15rem`. Spacing for the words is a different property, `word-spacing`.

### 4. Change the capitals

Add `text-transform` to the same rule:

```css
.tagline {
    font-style: italic;
    letter-spacing: 0.15rem;
    text-transform: uppercase;
}
```

Save and look at the browser.

You should see: the tagline shows in capital letters, PLAN YOUR WEEK. Look at `index.html`. It still says `Plan your week`. CSS changed how it shows on the screen, and not what you wrote.

The values to choose from are `uppercase`, `lowercase`, `capitalize` (a capital letter at the start of each word) and `none`. Try each one, and put it back to `uppercase`.

### 5. Make the button bold

Add `font-weight` to the `.btn` rule, under `font-size`:

```css
.btn {
    background-color: #2350c8;
    color: white;
    border: none;
    border-radius: 6px;
    padding: 0.6rem 1.2rem;
    font-size: 1rem;
    font-weight: bold;
    cursor: pointer;
}
```

Save and look at the browser.

You should see: the words on the button are bold.

Your heading is bold too, but you never asked for that. The browser gives every `h1` `font-weight: bold` as its default look, like the big size you saw in lesson 1.2. Add `font-weight: normal;` to the `h1` rule.

You should see: the heading turns light. Delete that line again, so the heading is bold.

### 6. Cross it out

Add `text-decoration` to the `.muted` rule, just to try it:

```css
.muted {
    color: dimgray;
    font-size: 1rem;
    text-decoration: line-through;
}
```

Save and look at the browser.

You should see: the tagline and the note both have a line through them. Both tags have the class `muted`, so both got it. In your app a finished homework item will look like this.

Try `underline` and `overline`, and then `none`. A link on a page gets an underline from the browser, and `text-decoration: none` takes it away. You will use that in the top bar.

Now delete the `text-decoration` line from `.muted`, so both lines look normal again.

### 7. Check your files

`index.html` did not change in this lesson. `style.css`:

```css
body {
    background-color: lightyellow;
    text-align: center;
    color: darkslategray;
    font-family: Georgia, serif;
    line-height: 1.5;
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
}
```

### 8. Save it

Save your work with the routine, and push it. The caption is `2.3 Make text look right`. The [git cheatsheet](../reference/01-git-cheatsheet.md) has the commands.

## Recap

- `line-height` is the height of a line. A number with no unit is a multiple of the text size.
- `letter-spacing` is the space between letters.
- `text-transform` changes the capitals on the screen: `uppercase`, `lowercase`, `capitalize` or `none`. Your HTML does not change.
- `font-weight` is `normal` or `bold`. The browser gives `h1` bold by default.
- `text-decoration` puts a line through, under or over the text, or takes it away with `none`.
- Put a property on `body` to give it to every line. Put it on a class to give it to some tags.

## Homework

Each should take about five minutes.

1. **Your own type.** Choose a `line-height` for the whole page, such as `1.2`, `1.5` or `1.8`. Then give the tagline your own look with `letter-spacing` and `text-transform`. Keep every line easy to read. You know it worked when the tagline looks like yours, and the other lines did not change except for the line-height. Before the next lesson, put `line-height` and the `.tagline` rule back as they are in step 7.

2. **Predict, then check.** For each change below, first write down what you will see. Then try it, and take it out again.

   ```css
   /* a */  .muted   { text-transform: capitalize; }        add this line to your .muted rule
   /* b */  body     { line-height: 3; }                      change the line in your body rule
   /* c */  .tagline { letter-spacing: -0.1rem; }            change the line in your .tagline rule
   /* d */  .btn     { text-decoration: underline; }         add this line to your .btn rule
   ```

   In (a) look at the tagline and at the note. They both have the class `muted`. You know it worked when you got at least three right, and you can say why the tagline still shows in capitals. Hint: the tagline has two classes, and they disagree. Lesson 2.1 says which one wins.

3. **Stretch: a finished item.** Your app will cross out homework that is done. Write a `.done` class with `text-decoration: line-through;` and `color: darkgray;`. Give it to the note: `<p class="muted done">Made by Sam</p>`. You know it worked when the note is crossed out and lighter than before. If it is crossed out but still dark grey, move `.done` below `.muted`, and say why. When you are done, take the `.done` rule out of `style.css` and put the note back to `class="muted"`.

## Stuck?

- **Nothing changes when I add `line-height`.** Check that the line is inside the `body` rule, between the curly brackets, with a colon and a semicolon. The number has no unit: `1.5`, not `1.5px`.
- **The tagline is not in capitals.** CSS spells it `uppercase`. Check that the line is in the `.tagline` rule, and that the tag says `class="tagline muted"`.
- **The letters are not further apart.** The property is `letter-spacing`, with a hyphen. Check the unit: `0.15rem`.
- **The button is not bold.** Check that `font-weight: bold;` is inside the `.btn` rule, and that the button tag says `class="btn"`.
- **My button has a different font from the text.** That is normal. A button keeps the browser's own font until you ask for another one. To make it use the font of the page, add `font-family: inherit;` to the `.btn` rule.
- **Everything has a line through it.** The `text-decoration` line is still in `.muted`. Delete it.
- **The page did not update.** Check that Go Live is running and `style.css` is saved. A dot next to a file name in its tab means it is not saved.
