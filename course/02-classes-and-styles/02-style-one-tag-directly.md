# 2.2: Style one tag directly

About 15 minutes.

By the end of this lesson you will know a third way to style a page: writing the style straight onto a tag. You will see that it is the strongest of the three ways, and learn when to use it and when to leave it alone.

## The idea

You now know two ways to point a style at something:

```
  p { font-size: 1.5rem; }        a tag rule: reaches every p
  .muted { color: dimgray; }      a class rule: reaches every tag with the name
```

There is a third way. You can write the style on the tag itself, with the `style` attribute. (An attribute is a word with a value in quotes, written inside an opening tag, like `class="muted"`.) There is no selector, because the style is already on the tag it is for:

```
  <p style="font-weight: bold; color: firebrick;">Welcome, Sam</p>
          |  |                                 |
          |  |                                 +- the style ends at the closing quote
          |  +----------------------------------- properties and values, with semicolons
          +-------------------------------------- the attribute
```

Inside the quotes you write properties and values the same way as in a CSS rule. There are no curly brackets. `font-weight: bold` makes the letters thick.

A style written on the tag is called an **inline style**. It is the strongest of the three:

```
  strongest   style="..." on the tag      reaches that one tag
              .name { ... }               reaches the tags with the name
  weakest     p { ... }                   reaches every tag of the kind
```

When two of them disagree, the stronger one wins, wherever the rules are in the file. When two rules are the same kind, such as two classes, neither is stronger, and the one lower in the file wins. You saw that in lesson 2.1.

New words:

- **attribute**: extra information inside an opening tag, like `class="muted"` or `style="..."`.
- **inline style**: a style written in a tag's `style` attribute.

## Steps

### 1. Start from last time

Open your project in VS Code and make sure Go Live is running. You will change `index.html` today, and `style.css` only a little.

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

### 2. Style one tag directly

Add a `style` attribute to the welcome line:

```html
<p style="font-weight: bold;">Welcome, Sam</p>
```

Save and look at the browser.

You should see: the welcome line is bold. Nothing else changed, and you did not touch `style.css`.

### 3. Write more than one property

Add a colour. Separate the properties with a semicolon:

```html
<p style="font-weight: bold; color: firebrick;">Welcome, Sam</p>
```

Save and look at the browser.

You should see: the welcome line is bold and red. It is still only that one line.

### 4. See which one wins

Give the note an inline colour. It already has a class that says `dimgray`:

```html
<p class="muted" style="color: firebrick;">Made by Sam</p>
```

Save and look at the browser.

You should see: the note is red. The class `.muted` says `dimgray`, the inline style says `firebrick`, and the inline style wins.

Now try to beat it. In `style.css`, move the `.muted` rule to the very bottom of the file, or to the very top, and save.

You should see: the note is still red. Where the rule sits does not matter here, because an inline style is stronger than a class.

### 5. See the cost

Say you want the tagline red too. Copy the style onto it:

```html
<p class="tagline muted" style="color: firebrick;">Plan your week</p>
```

Save and look at the browser.

You should see: both lines are red.

Now say you want to change the red to `teal`. You have to find every `style` and change each one. You have two now. A real page can have fifty.

Compare that with a class. If both lines had `class="accent"` and one rule said `.accent { color: firebrick; }`, you would change one word, in one place.

### 6. Take the experiments away

Delete all three `style` attributes you added, so the lines look like they did at the start:

```html
<p>Welcome, Sam</p>
<p class="tagline muted">Plan your week</p>
<button class="btn">Continue</button>
<p class="muted">Made by Sam</p>
```

In `style.css`, move the `.muted` rule back, directly under the `p` rule and above `.tagline`, where it was before step 4.

Save and look at the browser.

You should see: the page as it was at the start of the lesson.

An inline style is a good tool for trying something out quickly, or for one tag that is truly one of a kind. For a look you want to keep, or use twice, write a class.

You will meet inline styles again when you write JavaScript. It changes a page while it is running by setting a tag's style from the code.

### 7. Check your files

Nothing changed in the end, so your two files are as they were at the start of the lesson. `index.html` should still have this inside the `body`:

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

### 8. Save it

Save your work with the routine, and push it. The caption is `2.2 Style one tag directly`. The [git cheatsheet](../reference/01-git-cheatsheet.md) has the commands.

## Recap

- You can style a tag directly with the `style` attribute: `style="color: firebrick;"`.
- Inside the quotes you write properties and values with semicolons, and no curly brackets.
- An inline style reaches only its own tag.
- It is stronger than a class, and a class is stronger than a tag rule. Where a rule sits in the file does not change that.
- To change a look that many tags share, you would have to change every inline style. A class changes it in one place.
- Use an inline style to try something quickly. Keep the looks you want in the CSS file, in classes.

## Homework

Each should take about five minutes.

1. **Who wins?** Add `color: seagreen;` to the `p` rule in `style.css`. Now put `style="color: firebrick;"` on the note only. Before you look, write down the colour of each of these: the welcome line, the tagline, which has the class `muted`, and the note. Then check. You know it worked when you got all three right, and you can say which of the three ways of styling decided each colour. Take the colour out of the `p` rule and the inline style off the note when you are done.

2. **From inline to class.** Put `style="font-weight: bold; color: firebrick;"` on the welcome line. Then turn it into a class: delete the `style` attribute, write an `.accent` rule with the same two properties, and give the welcome line `class="accent"`. You know it worked when the page looks the same and there is no `style=` left in `index.html`. When you are done, take the `.accent` rule out of `style.css` and the `class="accent"` off the welcome line, so the line is `<p>Welcome, Sam</p>` again.

3. **Stretch: fix a friend's page.** A friend wrote this:

   ```html
   <p style="color: gray; font-size: 1rem;">Made by Sam</p>
   <p style="color: gray; font-size: 1rem;">Version 1</p>
   <p style="color: gray; font-size: 1rem;">Contact</p>
   ```

   Paste the three lines into `index.html`, under the note, and rewrite them with a class and a rule in `style.css`. Then say what you would change to make all three lines dark grey, and how many places you would touch before and after. You know it worked when the three lines share one class and one rule. When you are done, take the three lines and your rule out again.

4. **Stretch: who wins, live.** Open the [DevTools cheatsheet](../reference/04-devtools-cheatsheet.md). Pick the note, `<p class="muted">Made by Sam</p>`, find the crossed-out line in the Styles pane, and say which rule crossed it out and why. Then click inside `element.style` at the top of the Styles pane and type `color: seagreen`. You know it worked when the note turns green, the `color` line in `.muted` is crossed out, and you can say why an inline style beats a class.

## Stuck?

- **The inline style does nothing.** Check the quotes: `style="color: firebrick;"`, with a closing quote. Check that the property is spelled right, and that you used a colon `:` between the property and its value, and a semicolon `;` after the value.
- **Only the first property works.** Separate the properties with a semicolon: `style="font-weight: bold; color: firebrick;"`.
- **You used curly brackets.** Inside a `style` attribute there are none. Write `style="color: red;"`, not `style="{ color: red; }"`.
- **A class stopped working.** A tag can have an inline style and a class together. The inline style wins where they disagree. Delete the property from the `style` attribute and the class takes over again.
- **The page did not update.** Check that Go Live is running and `index.html` is saved. A dot next to a file name in its tab means it is not saved.
