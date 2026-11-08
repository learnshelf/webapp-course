# 1.2: Hello, HTML and CSS

About 20 minutes.

By the end of this lesson you will have a web page with your project title and a welcome line, centred on a coloured background, and you will know the difference between the two things that build every web page: HTML and CSS.

## The idea

A web page is made of three jobs:

```
  HTML                    CSS                     JavaScript
  what is on the page     how it looks            what happens
                          and where it sits       when you click

  <h1>Hello</h1>          h1 { color: red; }      (later)
```

Today is HTML and CSS. JavaScript comes later.

HTML stands for HyperText Markup Language, and CSS for Cascading Style Sheets. You do not need to remember the long names. They only tell you what the letters mean.

HTML is made of **tags**. A tag is a word in angle brackets. Most tags come in pairs, with content in between:

```
  <h1>Student Planner</h1>
  |   |              |
  |   |              +- closing tag (it has a slash)
  |   +---------------- the content
  +-------------------- opening tag
```

Here is the surprise of this lesson. Tags say **what** a piece of content is. They do not change how the page looks. To change how it looks, you use CSS. You will see it for yourself.

## Steps

### 1. See where you are going

Your teacher will open the finished app on screen. Click around and have a look.

The app starts with a front door, a landing page. Over the next lessons you will build it:

```
+--------------------------------------------+
|                                            |
|              Student Planner               |
|                                            |
|               Welcome, Sam                 |
|                                            |
|               [ Continue ]                 |
|                                            |
+--------------------------------------------+
```

Today you build the first piece: the title and the welcome line, centred on a coloured page.

### 2. Make the page

In VS Code, make a new file called `index.html` in your `studentplanner` folder, next to `README.md`.

Click in the empty file, type `!` and press Tab. (This shortcut is called Emmet, and VS Code has it built in.)

You should see: VS Code fills the file with the skeleton of a web page. It looks something like this:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>

</body>
</html>
```

If nothing happens when you press Tab, type the skeleton above by hand, exactly as it is shown.

You do not need to understand the top part yet. Everything you can see on the page goes between `<body>` and `</body>`.

### 3. Add your content

Type these two lines between `<body>` and `</body>`. Use your own first name instead of Sam:

```html
<body>
    <h1>Student Planner</h1>
    <p>Welcome, Sam</p>
</body>
```

`h1` is the main heading. `p` is a paragraph.

VS Code may add the closing tag for you as soon as you type an opening tag: type `<h1>` and `</h1>` may appear by itself. If it does, type only the words in between, and do not type the closing tag yourself.

Save the file with Ctrl+S (Cmd+S on a Mac).

### 4. Open it in the browser

Look at the blue bar at the very bottom of VS Code. Click **Go Live** at the bottom right. (If you cannot see it, look at "Stuck?" at the end.)

You should see: your browser opens with your page in it. The address starts with `127.0.0.1:5500`. That is your own computer showing you the page, and it is not on the internet. While it runs, the Go Live button changes to say `Port: 5500`.

If the page opens in a browser other than Chrome or Edge (a Mac may open Safari), copy the address from its address bar, paste it into Chrome or Edge, and use that browser from now on.

Put VS Code and the browser side by side if you can. From now on, every time you save a file, the page in the browser updates by itself:

```
  +------------------------------+      +------------------------------+
  | VS Code: index.html          |      | Browser: 127.0.0.1:5500      |
  +------------------------------+      +------------------------------+
  |                              |      |                              |
  | <h1>Student Planner</h1>     | save | Student Planner              |
  | <p>Welcome, Sam</p>          | ---> | Welcome, Sam                 |
  |                              |      |                              |
  +------------------------------+      +------------------------------+
```

Try it. Change the word `Welcome` to `Hello`, press Ctrl+S (Cmd+S on a Mac), and watch the browser. Then change it back and save again.

This is what your page looks like in the browser:

```
+------------------------------------------------+
| Document                                    x  |
+------------------------------------------------+
|                                                |
|  Student Planner  <- big and bold              |
|  Welcome, Sam                                  |
|                                                |
+------------------------------------------------+
```

Nobody told the heading to be big and bold. The browser gives every tag a plain default look. Remember that.

If the page ever does not update, refresh it by hand: F5, or Cmd+R on a Mac.

### 5. Wrap it in main

Put a `main` tag around both lines:

```html
<body>
    <main>
        <h1>Student Planner</h1>
        <p>Welcome, Sam</p>
    </main>
</body>
```

Save and look at the browser.

You should see: nothing changed. `main` says "this is the main part of the page". It is a label, and labels do not change how things look.

### 6. Try other tags

Change `main` to `div` in both places, the opening tag and the closing tag. Save and look at the browser.

Then change it to `section`. Save and look again.

You should see: the page looks the same every time. Put `main` back when you are done.

Careful: this is true for wrapper tags like `main`, `div` and `section`. Text tags like `h1` do come with a default look. If you change `h1` to `p`, the heading shrinks, because the browser styles `p` differently. That is the browser's default look, not the tag changing the page.

### 7. Change the look with CSS

Make a new file called `style.css`, next to `index.html`.

Now tell the page to read it. In `index.html`, add one line to the `head`, under the `title`:

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link rel="stylesheet" href="style.css">
</head>
```

Type this in `style.css`:

```css
body {
    background-color: lightyellow;
}
```

A CSS rule has three parts:

- `body` is the **selector**: which tag to style.
- `background-color` is the **property**: what to change.
- `lightyellow` is the **value**: what to change it to.

Save both files and look at the browser.

You should see: the page has a pale yellow background.

### 8. Centre the content

Right now the text hugs the left edge. Add a second line to the same rule in `style.css`:

```css
body {
    background-color: lightyellow;
    text-align: center;
}
```

A rule can hold as many lines as you like. Each line is a property and a value, and each ends with a semicolon.

Save and look at the browser.

You should see: the title and the welcome line move to the middle of the page, left to right.

```
+------------------------------------------------+
| Document                                    x  |
+------------------------------------------------+
|                                                |
|                Student Planner                 |
|                  Welcome, Sam                  |
|                                                |
+------------------------------------------------+
```

It is centred across, but it still sits at the top. Getting it into the middle from top to bottom as well is a bigger job, and you will do it in a later lesson.

### 9. Compare

You changed the tags, and nothing happened. You changed the CSS, and the page changed:

```
  change the tags (main -> div)    the page looks the same
  change the CSS (one line)        the page looks different
```

That is the difference between HTML and CSS. HTML says what is on the page. CSS says how it looks.

### 10. Check your files

These are your two files at the end of the lesson. Compare them with yours if something is not working.

`index.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <main>
        <h1>Student Planner</h1>
        <p>Welcome, Sam</p>
    </main>
</body>
</html>
```

`style.css`:

```css
body {
    background-color: lightyellow;
    text-align: center;
}
```

## Recap

- HTML is tags. They say what each piece of content is.
- Wrapper tags like `main`, `div` and `section` do not change how the page looks.
- CSS changes the look. A rule is a selector, then properties with values, and a rule can hold several of them.
- `text-align: center` centres text from left to right.
- The page reads your CSS because of the `link` line in the `head`.
- Save, and the browser shows every change by itself. That is Go Live at work.

Next you will save this page with git, and learn to look back at your save points, in [lesson 1.3](03-git-workflow.md). After it comes [lesson 1.4, Colour and type](04-colour-and-type.md).

## Homework

Each task should take about five minutes.

Lesson 1.3's homework asks you to save this homework with git. If you do that, do it first. Then take each change out again, as the end of each task says: the next lessons expect your files to look as they did at the end of this lesson.

1. **Pick your colour and your side.** Try at least three colour names for the background, such as `lavender`, `skyblue` and `tomato`, and pick your favourite. Then try `left` and `right` instead of `center` for `text-align`. You know it worked when the page shows your colour and the text sits where you want it. Take it out again when you are done: put the background back to `lightyellow` and `text-align` back to `center`.

2. **One more line.** Add a second `p` under the welcome line, saying what month you started. Then change `main` to `section` and look at the browser. You know it worked when you have two lines on the page, and changing the wrapper changed nothing. Take it out again when you are done: delete the second `p` line, and change `section` back to `main`, in both places.

3. **Stretch: your own rule.** Write a second rule in `style.css` that makes the welcome line a different colour. Hint: the selector is `p`, and the property for text colour is `color`. You know it worked when only the `p` text changes colour and the heading stays black. Take it out again when you are done: delete the `p` rule.

## Stuck?

- **Nothing changes in the browser.** Check that you saved the file. A dot next to the file name in its tab means it is not saved. If it is saved and nothing happens, refresh by hand: F5, or Cmd+R on a Mac.
- **There is no Go Live button.** The Live Server extension is missing. Click the Extensions icon on the left (it looks like four squares), search for `Live Server`, choose the one by Ritwick Dey, and click Install. Then look for Go Live again.
- **The browser says it cannot reach the site.** The live server has stopped. Click Go Live again.
- **The colour does not change.** Check the `link` line in `index.html`: `href="style.css"`. Both files must be in the same folder. In `style.css`, check the curly brackets `{ }` and that the line ends with a semicolon `;`.
- **The page looks strange or some text is missing.** Every paired tag needs a closing tag with a slash, like `</h1>` (`meta` and `link` do not). Check that each pair matches. VS Code may have added a closing tag for you as you typed, so look for a doubled one such as `</h1></h1>`, and delete the extra.
- **Pressing Tab after the `!` does nothing.** Type the skeleton from step 2 by hand.
