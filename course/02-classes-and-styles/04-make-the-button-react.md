# 2.4: Make the button react

About 20 minutes.

By the end of this lesson your button will turn darker when the mouse is over it, darker still while it is pressed, and fade smoothly between the colours. You will meet your first **pseudo-class**: a style that applies only while something is happening to a tag.

## The idea

Right now your button looks the same whatever the mouse does. A page feels alive when it answers the mouse. CSS can do that by itself, with no JavaScript. You add a colon and a word after a class name:

```
  .btn { ... }          the button, always
  .btn:hover { ... }    the button, while the mouse is over it
  .btn:active { ... }   the button, while it is being pressed
      |
      +-- no space before the colon
```

The word after the colon is a **pseudo-class**. You do not write it in the HTML. The browser knows when the mouse is over a tag, and it switches the rule on and off by itself.

One thing to remember: a phone has no mouse, so hover never shows there. A hover look is a nice extra, and it must never be the only way to tell that something is a button.

New words:

- **pseudo-class**: a condition added to a selector with a colon, like `:hover`.
- **hover**: the mouse pointer is over the tag.
- **active**: the tag is being pressed, with the mouse button held down.
- **transition**: a change that takes time, so it fades instead of jumping.

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

`style.css` should end with these three classes. Your colours may be different, and that is fine:

```css
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

Move the mouse over the button.

You should see: the pointer turns into a hand, and that is all. The button itself does not change.

### 2. Change the button when the mouse is over it

Add a new rule at the bottom of `style.css`. It is for the same class, with `:hover` after it:

```css
.btn:hover {
    background-color: #1c3f9c;
}
```

Save, then move the mouse onto the button and off it again.

You should see: the button turns a darker blue while the mouse is over it, and goes back when the mouse leaves. You did not change `index.html`, and the button still says `class="btn"`.

### 3. Change it again while it is pressed

Add another rule under it:

```css
.btn:active {
    background-color: #142f78;
}
```

Save. Move the mouse onto the button, then press the mouse button and hold it down.

You should see: the button turns darker again while you hold the mouse button, and goes back to the hover colour when you let go. The click does nothing else yet. It gets its job in a later lesson.

### 4. See why the order matters here

Move the whole `.btn:active` rule above the `.btn:hover` rule. Save, then press and hold on the button again.

You should see: it no longer gets darker when you press. While you press, the mouse is also over the button, so both rules apply. They are the same kind of rule, so the one lower in the file wins, and now that is `:hover`. This is the rule from lesson 2.1 again: when two rules are the same strength, the later one wins.

Move `.btn:active` back under `.btn:hover`.

### 5. See where order does not matter

Now move the `.btn:hover` rule above the `.btn` rule. Save and move the mouse over the button.

You should see: it still turns darker. A rule that names the class and a condition, `.btn:hover`, is a little stronger than a rule that names only the class, `.btn`. The stronger rule wins wherever it is in the file.

Move `.btn:hover` back to where it was, under `.btn`.

### 6. Make it fade

The colour jumps from one blue to the other. Add a `transition` line to the `.btn` rule, under `cursor`:

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
    transition: background-color 0.2s;
}
```

Save and move the mouse on and off the button.

You should see: the colour fades in a fifth of a second, both when the mouse arrives and when it leaves. `transition` says: when this property changes, take this long to do it. Try `1s` to watch it slowly, then put it back to `0.2s`.

### 7. Check your files

`index.html` did not change in this lesson. The end of `style.css` is:

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
    transition: background-color 0.2s;
}

.btn:hover {
    background-color: #1c3f9c;
}

.btn:active {
    background-color: #142f78;
}
```

### 8. Save it

Save your work with the routine, and push it. The caption is `2.4 Make the button react`. The [git cheatsheet](../reference/01-git-cheatsheet.md) has the commands.

## Recap

- A pseudo-class is a colon and a word after a selector. `.btn:hover` is the button while the mouse is over it, and `.btn:active` is the button while it is pressed.
- You do not write a pseudo-class in the HTML. The browser switches it on and off.
- `:hover` and `:active` are the same strength, so the later one in the file wins. Put `:active` under `:hover`.
- `.btn:hover` is stronger than `.btn`, so it wins wherever it is in the file.
- `transition: background-color 0.2s` makes a change fade. Put it on the normal rule, so it fades both ways.
- A phone has no mouse, so hover is only an extra.

## Homework

Each should take about five minutes.

1. **Your own button.** Change the three blues to colours that go with the button you designed in lesson 2.1. Keep the white words easy to read in all three. You know it worked when the button changes in three clear steps, resting, hover and pressed, and you can read the words every time. Before the next lesson, put the three blues back as they are in step 7, or keep your colours in a copy somewhere else.

2. **Hover on another tag.** `:hover` works on any tag, not only buttons. Add `.muted:hover { color: firebrick; }` and move the mouse over the tagline and the note. You know it worked when each grey line turns red while the mouse is over it. Then delete the rule again.

3. **Stretch: the quiet button.** If you made the second button in the lesson 2.1 homework, `<button class="btn quiet">`, and took it out again, put it and its `.quiet` rule back now. Move the mouse over it. It gets a dark blue box with blue words, and you can hardly read them. Say why: which of the two rules is stronger, `.btn:hover` or `.quiet`? Fix it with a `.quiet:hover` rule that sets a light background, such as `#dbe6ff`. You know it worked when the quiet button gets a light blue box when the mouse is over it. If it stays dark, move `.quiet:hover` below `.btn:hover`, and say why. When you are done, take the second button, the `.quiet` rule and the `.quiet:hover` rule out again.

## Stuck?

- **Nothing happens when the mouse is over the button.** Check that there is no space before the colon: `.btn:hover`, not `.btn :hover`. Check the spelling, and that the button says `class="btn"`.
- **It darkens on hover but not when I press.** The `.btn:active` rule has to be below the `.btn:hover` rule.
- **The colour jumps and does not fade.** Check that the `transition` line is inside the `.btn` rule, with a semicolon, and that it says `background-color 0.2s`.
- **I cannot hold the mouse down and look at the same time.** Press and hold, look at the button, then let go. The [DevTools cheatsheet](../reference/04-devtools-cheatsheet.md) shows how the browser's tools can hold a state for you.
- **There is no hover on my phone.** That is right. A phone has no mouse.
- **The page did not update.** Check that Go Live is running and `style.css` is saved. A dot next to a file name in its tab means it is not saved.
