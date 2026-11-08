# CSS cheatsheet

The CSS you will use most, grouped by job. To try a style in the browser before you write it, see the [DevTools cheatsheet](04-devtools-cheatsheet.md).

## A rule

```css
.muted {
    color: dimgray;
    font-size: 1rem;
}
```

- `.muted` is the **selector**: which tags the rule is for.
- `color: dimgray;` is a **property** and its **value**, with a semicolon at the end. A rule can have as many as you like.

## Selectors: which tags

| Write | Which tags |
|---|---|
| `p { }` | every `p` tag |
| `.muted { }` | every tag with `class="muted"` |
| `h1, h2 { }` | both kinds of tag |
| `.btn:hover { }` | the tag with `class="btn"`, while the mouse is over it |
| `.btn:active { }` | the same, while it is pressed |
| `.card h2 { }` | an `h2` inside a tag with `class="card"` |
| `#menu { }` | the one tag with `id="menu"` |

When two rules disagree about the same property, the stronger one wins:

```
  strongest   style="..." on the tag
              #name { ... }
              .name { ... }
  weakest     p { ... }
```

- Two rules of the same kind: the one lower in the file wins.
- `.btn:hover` is a little stronger than `.btn`, so it wins wherever it sits.
- `!important` after a value, as in `color: red !important;`, beats all of these. Use it only as a last resort: to override it later you need another `!important`.

Some properties pass down from a tag to the tags inside it, and some do not:

| Passes down | Does not pass down |
|---|---|
| `color`, `font-family`, `font-size`, `line-height`, `text-align` | `background`, `border`, `padding`, `margin` |

A tag takes the properties that pass down from the tag around it, such as `body`, unless it has a rule of its own. Buttons and form fields are an exception: they keep the browser's own font, whatever `body` says, until you write `font-family: inherit;` on them.

## Where CSS goes

| Write | Where |
|---|---|
| `<link rel="stylesheet" href="style.css">` | in the `head` of `index.html`: use this file |
| `<p style="color: red;">` | on one tag |
| `<style> ... </style>` | in the `head`: rules written inside the page itself |
| `/* a note to yourself */` | a comment in a CSS file |
| `/* color: red; */` | switch a line off without deleting it. Select the line and press Ctrl+/ (Cmd+/ on a Mac) |

With several stylesheets, the one linked later counts as lower in the file, so its rule wins when two rules are equally strong.

## Colours and backgrounds

| Write | What it does |
|---|---|
| `color: darkslategray;` | text colour |
| `background-color: lightyellow;` | the colour behind a tag |
| `background-color: #2350c8;` | a colour as hex: red, green and blue |
| `background-color: rgb(35, 80, 200);` | the same colour, in numbers from 0 to 255 |
| `background-color: hsl(224, 70%, 46%);` | the same colour as hue, saturation and lightness |
| `background-color: transparent;` | no colour at all |
| `background-image: url("sky.png");` | a picture behind a tag |
| `opacity: 0.5;` | the whole tag half see-through |

Names used in the app: `lightyellow`, `darkslategray`, `firebrick`, `dimgray`, `white`, `khaki`, `aliceblue`. Pick a text colour and a background colour that are far apart, or the text is hard to read.

## Fonts and text

| Write | What it does |
|---|---|
| `font-family: Georgia, serif;` | the font, then a back-up |
| `font-size: 1.5rem;` | how big |
| `font-weight: bold;` | `normal` or `bold` |
| `font-style: italic;` | `normal` or `italic` |
| `line-height: 1.5;` | the height of each line, as a multiple of the text size |
| `letter-spacing: 0.15rem;` | the space between letters |
| `text-transform: uppercase;` | `uppercase`, `lowercase`, `capitalize` or `none` |
| `text-decoration: underline;` | `underline`, `overline`, `line-through` or `none` |
| `text-align: center;` | `left`, `center` or `right` |

Font choices:

| Write | What you get |
|---|---|
| `font-family: Georgia, serif;` | letters with little feet |
| `font-family: Arial, sans-serif;` | plain letters |
| `font-family: system-ui, sans-serif;` | the font of the computer you are on |
| `font-family: "Courier New", monospace;` | every letter the same width |

A font name with a space in it needs quotes.

## Sizes

| Unit | What it is |
|---|---|
| `rem` | a multiple of the browser's text size: `1.5rem` is one and a half times |
| `px` | a fixed size in pixels, the same for everybody |
| `%` | a part of the space around: `width: 50%` |
| `vh` | one percent of the height of the window: `min-height: 100vh` |
| `fr` | one share of the free space in a grid: `repeat(3, 1fr)` is three equal columns |
| `s` | a time: `transition: background-color 0.2s` |
| no unit | a multiple of something: `line-height: 1.5` |

Use `rem` for text, so the person using the page decides.

## The box

Every tag is a box with four layers, from the inside out:

| Layer | What it is | Written with |
|---|---|---|
| content | the words, or the tags, inside | `width`, `max-width`, `min-height` |
| padding | the space inside the border. It has the tag's background colour | `padding` |
| border | a line around the padding | `border` |
| margin | the space outside the border. It has no colour of its own | `margin` |

| Write | What it does |
|---|---|
| `padding: 2rem;` | the space inside the tag |
| `border: 2px solid firebrick;` | a line around the tag: how thick, what kind (`solid`, `dashed` or `dotted`) and what colour |
| `border-radius: 12px;` | round corners |
| `border-bottom: 2px solid khaki;` | a line on one side only |
| `margin: 1rem;` | the space outside the tag |
| `margin-top: 0;` | one side only. The sides are `-top`, `-right`, `-bottom` and `-left`, and `padding` and `border` have them too |
| `box-shadow: 0 4px 12px darkgray;` | a shadow: how far across, how far down, how blurry, what colour. It takes up no room |
| `width: 7rem;` | how wide |
| `width: 100%;` | as wide as the space around |
| `max-width: 40rem;` | no wider than this |
| `min-height: 100vh;` | at least as tall as the window |
| `margin: 0 auto;` | with a `width` or a `max-width`, the tag sits in the middle: no space above and below, and the same space left and right |
| `box-sizing: border-box;` | `width` then counts the padding and the border too. Without it, `width` is only the content, and the padding and the border are added to it |

The browser gives some tags margins of their own: `h1` and `p` have them, and `body` has 8 pixels until you write `margin: 0`. The [DevTools cheatsheet](04-devtools-cheatsheet.md) shows how to read them.

How a tag sits on the page is set with `display`:

| Write | What it does |
|---|---|
| `display: block;` | the tag takes the whole width and starts on a new line. `h1`, `p`, `div` and `main` are like this |
| `display: inline;` | the tag sits inside a line of text, like a word. `span` and `a` are like this. `width` and `height` do nothing on it |
| `display: inline-block;` | the tag sits in the line like a word, but it can have a width, a height and margins. `button` is like this |

`margin` and `padding` take one to four values:

| Write | Which sides |
|---|---|
| `padding: 1rem;` | all four sides |
| `padding: 0.5rem 1rem;` | top and bottom, then left and right |
| `padding: 1rem 2rem 3rem 4rem;` | top, right, bottom, left (clockwise) |

## Layout: flexbox

The [Flexbox and grid cheatsheet](05-flexbox-and-grid-cheatsheet.md) has all the values, with pictures and patterns.

| Write | What it does |
|---|---|
| `display: flex;` | the tag's children go in a row |
| `flex-direction: column;` | `row` or `column`: the main axis |
| `justify-content: center;` | where the children sit along the main axis |
| `align-items: center;` | where the children sit across it |
| `gap: 1rem;` | the space between the children |
| `flex-wrap: wrap;` | move to a new line when there is no room |
| `align-self: flex-end;` | one child places itself |
| `flex: 1;` | one child takes the space that is left |

The values for `justify-content` and `align-items` are `flex-start`, `center` and `flex-end`. `justify-content` also has `space-between`: the first child at one end and the last at the other. `align-items` also has `stretch`, which is the default. In a `row`, `justify-content` is left and right and `align-items` is up and down. In a `column` it is the other way round.

## Layout: grid

More in the [Flexbox and grid cheatsheet](05-flexbox-and-grid-cheatsheet.md).

| Write | What it does |
|---|---|
| `display: grid;` | the tag has rows and columns |
| `grid-template-columns: repeat(3, 1fr);` | three equal columns |
| `grid-template-columns: repeat(auto-fit, minmax(14rem, 1fr));` | as many columns as fit, none narrower than 14rem |
| `gap: 1rem;` | the space between the cells |

## Lists and links

| Write | What it does |
|---|---|
| `list-style: none;` | no bullets |
| `ul { margin: 0; padding: 0; }` | takes away the space the browser puts around a list and the indent |
| `color: darkslategray;` on `a` | the browser's blue becomes your colour |
| `text-decoration: none;` on `a` | no line under a link |

## Custom properties

| Write | What it does |
|---|---|
| `:root { --space-md: 1rem; }` | a name for a value, available in every rule. The name starts with two hyphens |
| `gap: var(--space-md);` | use the value |

Change the value in `:root`, and everything that uses it changes.

## Layout classes in the Student Planner

These are classes written in the Student Planner's `layout.css`. They say where the children of a tag go, and how much space and width it gets. Put them on the tag, beside its look class: `class="row gap-md align-center card"`.

| Class | What it does |
|---|---|
| `column` | the children are stacked |
| `row` | the children are side by side |
| `grid` | the children are in as many columns as fit |
| `justify-between` | the first child at one end, the last at the other |
| `justify-center` | the children in the middle along the main axis |
| `align-center` | the children in the middle across it |
| `width-fill` | this child takes the space that is left |
| `gap-xs`, `gap-sm`, `gap-md` | the space between the children, from the scale |
| `padding-md`, `padding-lg`, `padding-xl` | the space inside the tag, from the scale |
| `width-lg` | no wider than 48rem |
| `center-self` | a tag that is narrower than its parent sits in the middle |

## Look classes in the Student Planner

These are in the Student Planner's `style.css` and say how a tag looks. A tag can have several: `class="card roomy accent"`.

| Class | What it does |
|---|---|
| `card` | a white box with a line and round corners. It has no room inside: add a `padding-` class |
| `roomy` | room around a card, a margin of 1rem: use it with `card` |
| `accent` | changes the line colour of a card to red: use it with `card` |
| `title` | a bold name |
| `time` | a time in grey typewriter letters |

## Mouse and movement

| Write | What it does |
|---|---|
| `cursor: pointer;` | a hand when the mouse is over the tag |
| `.btn:hover { ... }` | a look for while the mouse is over the tag |
| `.btn:active { ... }` | a look for while it is pressed |
| `transition: background-color 0.2s;` | a change takes this long, so it fades |

## Showing and hiding

| Write | What it does |
|---|---|
| `display: none;` | the tag is not on the page at all |
| `position: sticky; top: 0;` | the tag stays in view when the page scrolls |
| `overflow: auto;` | a scrollbar when the content is too big |

## Also useful

```css
/* the same idea for colours */
:root { --blue: #2350c8; }
.btn { background-color: var(--blue); }

/* rules that only apply on a narrow screen */
@media (max-width: 40rem) {
    .menu { display: none; }
}

/* rules for people who use a dark theme */
@media (prefers-color-scheme: dark) {
    :root { --page: #1b1b1b; }
}
```
