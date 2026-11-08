# HTML cheatsheet

The HTML you will use most, grouped by job.

## How a tag is written

```
  <p class="muted">Words</p>
   |  |            |    |
   |  |            |    +- the closing tag has a slash
   |  |            +------ the content
   |  +------------------- an attribute: name="value"
   +---------------------- the tag name
```

An attribute goes inside the opening tag.

- Tags come in pairs, and the second one has a slash. Close them in the reverse order you opened them.
- A few tags have no content, so they have no closing tag: `<br>`, `<hr>`, `<img>`, `<input>`, `<meta>` and `<link>`.
- Write tag names and attribute names in lower case, and put attribute values in quotes.
- A comment is ignored by the browser: `<!-- a note to yourself -->`.
- To show a `<`, `>` or `&` on the page, write `&lt;`, `&gt;` or `&amp;`.

## The page

| Write | What it does |
|---|---|
| `<!DOCTYPE html>` | this is a modern web page |
| `<html lang="en">` | the whole page, and its language |
| `<head> ... </head>` | information about the page |
| `<body> ... </body>` | everything you can see |

What goes in the `head`:

| Write | What it does |
|---|---|
| `<meta charset="UTF-8">` | how the letters are stored |
| `<meta name="viewport" content="width=device-width, initial-scale=1.0">` | a phone uses its real width |
| `<title>Student Planner</title>` | the name in the browser tab |
| `<link rel="stylesheet" href="style.css">` | use this CSS file |
| `<link rel="icon" type="image/svg+xml" href="favicon.svg">` | the small icon in the tab |
| `<script src="app.js" defer></script>` | use this JavaScript file. `defer` makes it wait until the whole page has been read |

Without `defer`, a script in the `head` runs before the `body` exists, and it cannot find anything on the page.

## Text

| Write | What it does |
|---|---|
| `<h1>Student Planner</h1>` | the main heading, one per page |
| `<h2>` to `<h6>` | smaller headings, in order |
| `<p>Welcome, Sam</p>` | a paragraph |
| `<strong>text</strong>` | important text, bold by default |
| `<em>text</em>` | stressed text, italic by default |
| `<span>text</span>` | a piece of text inside a line, for CSS to style |
| `<br>` | a line break |
| `<hr>` | a line across the page |

The browser gives each of these a default look, such as the big bold `h1`. CSS changes the look. Choose a tag for what the text is, not for how it looks.

## Sections: the frame of the page

| Write | What it is |
|---|---|
| `<header>` | the top of the page or of a part: the name, the menu |
| `<nav>` | a group of links |
| `<main>` | the main part of the page, one per page |
| `<section>` | one part of the page, usually with its own heading |
| `<article>` | a piece that makes sense on its own, such as one card |
| `<aside>` | a side note |
| `<footer>` | the bottom of the page or of a part |
| `<div>` | a box with no meaning, only for layout and style |

Most of these do not change how the page looks. They tell the browser what each part is. A page often looks like this:

```html
<body>
    <header>
        <nav> ... the links ... </nav>
    </header>
    <main>
        <section>
            <h2>Activities</h2>
            <article> ... one card ... </article>
            <article> ... one card ... </article>
        </section>
    </main>
    <footer> ... </footer>
</body>
```

## Links, lists and pictures

| Write | What it does |
|---|---|
| `<a href="https://example.com">text</a>` | a link to another page |
| `<a href="https://example.com" target="_blank">text</a>` | the same link, opened in a new tab |
| `<a href="homework.html">Homework</a>` | a link to another file of yours |
| `<a href="#schedule">Schedule</a>` | a link to the tag with `id="schedule"` on this page |
| `<ul> <li>one</li> <li>two</li> </ul>` | a bulleted list |
| `<ol> <li>one</li> <li>two</li> </ol>` | a numbered list |
| `<img src="club.jpg" alt="Chess club">` | a picture. Always write the `alt`: it says what the picture shows |

## Buttons

| Write | What it does |
|---|---|
| `<button>Continue</button>` | a button |
| `<button type="button">Add</button>` | does nothing by itself: JavaScript gives it a job |
| `<button type="submit">Save</button>` | sends the form it is in |

Inside a `<form>`, a button with no `type` submits the form, and the page reloads. Always write `type="button"` or `type="submit"` on a button in a form.

## Forms and inputs

A form is a group of inputs. Each input has a label that says what to type. Link them with `for` and `id`:

```html
<form>
    <label for="subject">Subject</label>
    <input id="subject" type="text" name="subject" placeholder="Maths">

    <label for="due">Due date</label>
    <input id="due" type="date" name="due">

    <label>
        <input type="checkbox" name="done"> Done
    </label>

    <button type="submit">Add</button>
</form>
```

### Form fields

Most fields are an `<input>`. Its `type` decides what it looks like and what it accepts. `<textarea>` and `<select>` are fields too, but they are not inputs:

| Write | What you get |
|---|---|
| `<input type="text">` | one line of text |
| `<input type="number">` | a number, with `min`, `max` and `step` |
| `<input type="date">` | pick a date |
| `<input type="time">` | pick a time |
| `<input type="email">` | an email address |
| `<input type="password">` | text shown as dots |
| `<input type="search">` | a search box |
| `<input type="checkbox">` | a box to tick: on or off |
| `<input type="radio">` | one choice out of a group (the group shares one `name`) |
| `<input type="range">` | a slider |
| `<input type="color">` | pick a colour |
| `<textarea></textarea>` | many lines of text |
| `<select> <option value="mon">Monday</option> </select>` | a drop-down list |

### Attributes that fields use

| Write | What it does |
|---|---|
| `name="due"` | the name of the value, when the form is sent |
| `value="Maths"` | the starting value |
| `placeholder="Maths"` | grey hint text that disappears when you type |
| `required` | the form cannot be sent without it |
| `disabled` | the input cannot be used |
| `checked` | a checkbox or radio that starts ticked |
| `min="0" max="10"` | the smallest and largest number or date |
| `for="due"` | on a label: the `id` of the input it belongs to |

## Tables

For a schedule, or a list of items with columns:

```html
<table>
    <thead>
        <tr><th>Time</th><th>Class</th></tr>
    </thead>
    <tbody>
        <tr><td>09:00</td><td>Maths</td></tr>
        <tr><td>10:00</td><td>History</td></tr>
    </tbody>
</table>
```

| Write | What it is |
|---|---|
| `<table>` | the table |
| `<thead>` | the heading rows, at the top |
| `<tbody>` | the other rows |
| `<tr>` | one row |
| `<th>` | a heading cell |
| `<td>` | a cell |

## Attributes any tag can have

| Write | What it does |
|---|---|
| `class="muted"` | a name for CSS to point at; several are separated by a space |
| `id="schedule"` | a name used once on the page, for links and JavaScript |
| `style="color: red;"` | a style written on the tag |
| `title="Delete"` | a small note that shows when the mouse waits over the tag |
| `hidden` | hides the tag |

## Also useful

| Write | What it does |
|---|---|
| `<dialog> ... </dialog>` | a window on top of the page, opened with JavaScript |
| `<script> ... </script>` | JavaScript |
