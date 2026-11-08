# 2.5: Centre the front door

About 35 minutes.

By the end of this lesson your front door, the title, the welcome line, the button and the lines around them, will sit in the middle of the window, left to right and top to bottom. You will write a class, as in lesson 2.1, and meet **flexbox**, the CSS tool for placing things.

## The idea

At the end of lesson 1.2 your page was centred left to right, but it still hugged the top. That lesson promised that getting it into the middle from top to bottom would come later. This is that lesson.

Here is why it hugs the top. The browser stacks tags one under the other, from the top, each on its own line. `text-align: center` centres the words inside each line, but nothing moves the lines down.

To place things, you tell a container how to arrange what is inside it. The container is a tag, and the tags directly inside it are its **children**. Your `main` will be the container, and the `h1`, the `p`, the `button` and the other lines are its children. You will point at it with a class, as in lesson 2.1.

`display: flex` turns a tag into a **flex container**, and its children follow the container's settings. Which way they line up depends on the direction:

```
  flex-direction: row                  flex-direction: column

  +-----+ +-----+ +-----+              +-----+
  |  1  | |  2  | |  3  |              |  1  |
  +-----+ +-----+ +-----+              +-----+
  main axis: left to right             +-----+
  cross axis: up and down              |  2  |
                                       +-----+
                                       +-----+
                                       |  3  |
                                       +-----+
                                       main axis: top to bottom
                                       cross axis: left and right
```

Two settings place the children, one along each axis:

```
  justify-content    places the children along the main axis
  align-items        places the children along the cross axis

                     in a row           in a column
  justify-content    left and right     up and down
  align-items        up and down        left and right
```

The same two settings swap jobs when the direction changes. You will see that for yourself in step 9.

New words:

- **flex container**: a tag with `display: flex`. Its children are placed by its settings.
- **child**: a tag directly inside another tag.
- **main axis** and **cross axis**: the direction the children follow each other, and the direction across it.
- **vh**: one percent of the height of the window. `100vh` is the whole height.

## Steps

### 1. Start from last time

Open your project in VS Code and make sure Go Live is running. You will change both files today.

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

`style.css` should end with your classes, `.muted`, `.tagline`, `.btn`, and the `.btn:hover` and `.btn:active` rules. Your colours and font may be different, and that is fine.

You should see: the front door centred left to right, at the top of the page.

### 2. Give the main a name

In `index.html`, add a class to the opening `main` tag:

```html
<main class="landing">
```

The name is yours to choose. `landing` fits, because this is the landing page of your app.

Save and look at the browser.

You should see: nothing changed. A name by itself changes nothing.

### 3. Make a rule for the name

Add this to the bottom of `style.css`:

```css
.landing {
    background-color: white;
}
```

The white is only there to help you see the box. You will take it away at the end.

Save and look at the browser.

You should see: a white band behind the front door, with yellow showing around it. The rest of the page stays yellow. The `.landing` rule styles only the `main` that has the name.

### 4. Make it a flex container

Add `display: flex` to the rule:

```css
.landing {
    background-color: white;
    display: flex;
}
```

Save and look at the browser.

You should see: the lines jump into one row, side by side, and the white box shrinks to the height of that row. Nobody told them to. A flex container puts its children in a row, and the children are the tags directly inside it. The button looks tall, because a row stretches its children to the height of the row unless you tell it otherwise. You will fix that in step 6. If your window is narrow, the lines squeeze together and some words wrap onto a second line. Zoom out with Ctrl and **-** (Cmd and **-** on a Mac) to see them all in one row. Press Ctrl+0 (Cmd+0) when you are done.

### 5. Stack them in a column

Add a direction:

```css
.landing {
    background-color: white;
    display: flex;
    flex-direction: column;
}
```

Save and look at the browser.

You should see: the lines are stacked again, one under the other. Look at the button. It has stretched across the whole width of the box. A flex container stretches its children across the cross axis unless you tell it otherwise. You will do that in the next step.

### 6. Centre across

Add `align-items`:

```css
.landing {
    background-color: white;
    display: flex;
    flex-direction: column;
    align-items: center;
}
```

Save and look at the browser.

You should see: the lines are centred left to right, and the button is back to its normal size. In a column the cross axis goes left and right, so `align-items` moved them along it. Nothing moved down, because the box is only as tall as its content, so there is no room to move in.

### 7. Make the box as tall as the window

Add a height to the rule. `min-height` means "at least this tall":

```css
.landing {
    background-color: white;
    display: flex;
    flex-direction: column;
    align-items: center;
    min-height: 100vh;
}
```

Save and look at the browser.

You should see: the white box grows to the height of the window, with a yellow strip around it, and the content is still at the top of the box. Scroll down a little: the page is now taller than the window, and on some computers a scrollbar shows on the right. That is because the browser leaves a little space around the body by default, so the page is taller than the window by that space, top and bottom.

Take that space away. Add one line at the top of the `body` rule:

```css
body {
    margin: 0;
    background-color: lightyellow;
    text-align: center;
    color: darkslategray;
    font-family: Georgia, serif;
    line-height: 1.5;
}
```

`margin` is the space around a tag. You will meet it properly in [lesson 2.6](06-the-box.md).

Save and look at the browser.

You should see: the strip is gone, the page no longer scrolls, and the white box fills the whole window.

### 8. Centre down

Now there is room to move in. Add `justify-content`:

```css
.landing {
    background-color: white;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
}
```

Save and look at the browser.

You should see: the front door sits in the middle of the window, both ways. In a column the main axis goes down, so `justify-content` moved the lines up and down.

### 9. Swap the jobs

Try the two settings one at a time.

Change `justify-content: center` to `justify-content: flex-end`. Save and look at the browser.

You should see: the stack drops to the bottom of the window, still centred left to right. In a column the main axis goes down.

Change it back to `center`. Now change `align-items: center` to `align-items: flex-end`. Save and look.

You should see: the stack moves to the right edge, still centred up and down. In a column the cross axis goes across.

Now change `flex-direction: column` to `flex-direction: row`. Keep `align-items: flex-end`. Save and look.

You should see: the lines sit side by side along the bottom of the window. The same `align-items: flex-end` that sent the stack to the right now sends the lines to the bottom, because in a row the cross axis goes up and down. If the lines do not all fit across, zoom out as in step 4.

```
  column                              row
  justify-content: up and down        justify-content: left and right
  align-items: left and right         align-items: up and down
```

Put everything back: `column`, and `center` in both.

### 10. Add the space between

Add `gap`, above `min-height`:

```css
.landing {
    background-color: white;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 1rem;
    min-height: 100vh;
}
```

`gap` is the space between the children. It is only between them, not around the outside.

Save and look at the browser.

You should see: a little more space between the lines. Try `3rem` to see it clearly, then put it back to `1rem`.

### 11. Take away the white

Delete the line `background-color: white;` from the `.landing` rule. Keep the one in `body`.

Save and look at the browser.

You should see: the yellow page again, with the front door in the middle. You only needed the white to see the box.

### 12. Look at it on a phone

Open the phone view like in lesson 1.4: press F12, then the phone-and-tablet icon, or Ctrl+Shift+M (Cmd+Shift+M on a Mac).

You should see: the same page in a narrow screen, still in the middle. The [DevTools cheatsheet](../reference/04-devtools-cheatsheet.md) shows what else this panel can do. Close it with F12 when you are done.

### 13. Check your files

`index.html` changed in one place. The `main` tag has a class:

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
    <main class="landing">
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
    margin: 0;
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
    transition: background-color 0.2s;
}

.btn:hover {
    background-color: #1c3f9c;
}

.btn:active {
    background-color: #142f78;
}

.landing {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 1rem;
    min-height: 100vh;
}
```

### 14. Save it

Save your work with the routine, and push it. The caption is `2.5 Centre the front door`. The [git cheatsheet](../reference/01-git-cheatsheet.md) has the commands.

## Recap

- By default the browser stacks tags from the top. `text-align` only centres the words inside each line.
- `display: flex` makes a tag a flex container, and its children follow its settings.
- `flex-direction` sets the main axis: `row` goes left to right, `column` goes top to bottom.
- `justify-content` places the children along the main axis. `align-items` places them along the cross axis. They swap jobs when the direction changes.
- `min-height: 100vh` makes a box at least as tall as the window, so there is room to centre in.
- `gap` is the space between the children.
- The [Flexbox and grid cheatsheet](../reference/05-flexbox-and-grid-cheatsheet.md) lists every value, with pictures.

## Homework

Each should take five to ten minutes. Work in your own `style.css`. If a row is too wide to fit across your window, zoom out with Ctrl and **-** (Cmd and **-** on a Mac).

1. **Nine places.** The front door can sit in nine places:

   ```
     top left       top centre      top right
     middle left    middle          middle right
     bottom left    bottom centre   bottom right
   ```

   Copy the table into a notebook. With `flex-direction: column`, write down which `justify-content` and which `align-items` each place needs. The values to choose from are `flex-start`, `center` and `flex-end`. Then try every place in the browser and correct your notes. Now change to `row` and test again. Hint: in a column, one of the two settings only ever picks top, middle or bottom. You know it worked when your table is right for both directions, and you can say which places need different values in a row. When you are done, put your own `.landing` rule back as it is in step 13.

2. **Predict, then check.** For each rule below, first write down where the lines will end up and how they are arranged. Only then try it. Keep `display: flex` and `min-height: 100vh` in the rule. `space-between` puts the first child at the start, the last at the end, and shares the space that is left between them.

   ```css
   /* a */  flex-direction: row;     justify-content: center;         align-items: flex-start;
   /* b */  flex-direction: column;  justify-content: flex-end;       align-items: flex-end;
   /* c */  flex-direction: row;     justify-content: space-between; align-items: center;
   /* d */  flex-direction: column;  justify-content: space-between; align-items: center;
   ```

   You know it worked when you got at least three right, and you can explain the others with the words main axis and cross axis. When you are done, put your own `.landing` rule back as it is in step 13.

3. **Fix a friend's page.** A friend wants their lines stacked and in the middle of the window, both ways. Their rule is below. First switch your own `.landing` rule off: select its lines in `style.css` and press Ctrl+/ (Cmd+/ on a Mac), which turns them into a comment. Then paste your friend's rule under it, and look at the result.

   ```css
   .landing {
       display: flex;
       justify-content: center;
       min-height: 100vh;
   }
   ```

   Fix it by adding two lines or fewer. The button must keep its normal size, so check that it is not stretched across the page. Then do the same for this one, which should also end up in the middle, both ways. Use it in place of the friend's first rule:

   ```css
   .landing {
       display: flex;
       flex-direction: column;
       align-items: center;
   }
   ```

   You know it worked when both pages show a stack in the middle of the window, and you can say which lines you added and which axis each of them works on. When you are done, delete the friend's rule and press Ctrl+/ (Cmd+/) on your own commented lines to switch them on again. Your rule must have `gap: 1rem;` in it, as in step 13.

4. **Switch off, switch on.** Open the [DevTools cheatsheet](../reference/04-devtools-cheatsheet.md). Pick `<main class="landing">` and switch off the six lines of the `.landing` rule one at a time: `display`, `flex-direction`, `align-items`, `justify-content`, `gap` and `min-height`. For each one, write one sentence about what the page does without it. Switch every line back on. You know it worked when you have six sentences and the page looks normal at the end.

5. **Stretch: one child moves.** Add `align-self: flex-end;` to your `.tagline` rule. `align-self` is `align-items` for one child. You know it worked when only the tagline moves to the right edge and everything else stays in the middle. Try `flex-start`, then try it with `row` in place of `column`, and say what changed. When you are done, take `align-self` out of the `.tagline` rule and put `column` back.

## Stuck?

- **Nothing moves when you add the rule.** Check that the name matches in both files: `class="landing"` in `index.html` and `.landing` in `style.css`, with the dot. Check the curly brackets `{ }` and that every line ends with a semicolon `;`.
- **The lines sit side by side.** That is what `display: flex` does on its own. Add `flex-direction: column`.
- **The button is as wide as the page.** Add `align-items: center`.
- **The content stays at the top.** `justify-content` can only move things if the box is taller than they are. Check that `min-height: 100vh` is in the `.landing` rule.
- **The page scrolls a little, or a scrollbar shows on the right.** Check that `margin: 0;` is in the `body` rule.
- **The page is white instead of yellow.** Delete `background-color: white;` from the `.landing` rule, and keep the one in `body`.
- **It is not where you expected.** Say which direction it is, `row` or `column`. That tells you which way the main axis goes. Then work out which of the two settings works along it.
- **Nothing is centred.** CSS spells it `center`, the American way. Also check that `align-items` and `justify-content` are inside the `.landing` rule.
- **The page did not update.** Check that Go Live is running, and that both files are saved. A dot next to a file name in its tab means it is not saved.
