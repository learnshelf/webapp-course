# Web app course: roadmap

A sketch of the whole course, to build on as the lessons are written. It is a draft, not a decision: change anything here that the lessons turn out to need. The site does not publish this file.

## What the student builds

Student Planner, a small app with three screens:

- **Schedule**: the classes of the day, with the current and the next class marked.
- **Homework**: items with a due date and a tick, and filters for all, not complete, due and overdue.
- **Activities**: weekly clubs as cards, and the next few times they happen.

It has a top bar that turns into a menu button on a phone, a light and a dark look, and it remembers what the student added.

The finished app runs on one loop, and the JavaScript chapters teach it step by step:

```text
  1. all data lives in one object, the state (lists of items)
  2. an action changes the state, then saves it and draws the page again
  3. render() rebuilds every list on the page from the state
```

## The chapters

| Ch | Name | At the end the student has | New ideas |
|---|---|---|---|
| 1 | Your first page (written) | a landing page: title, welcome line, plain button | tags, CSS rules, rem, head and body |
| 2 | Layout | the landing centred, a top bar, cards, a small layout kit of their own | classes, box model, flexbox, grid, custom properties, sticky |
| 3 | The three screens, static | schedule table, homework list, activity cards, forms, light and dark, phone width | table, form, input types, colour variables, `prefers-color-scheme`, media queries |
| 4 | JavaScript 1 | Continue works, tabs switch, the schedule drawn from an array, add and delete, kept after a refresh | script, DOM, events, arrays and objects, state and render, `localStorage` |
| 5 | JavaScript 2 | homework that ticks, filters and counts, overdue by date, an activity dialog, the upcoming list | dates, derived values, `<dialog>` |
| 6 | Finish | Now and Next marks, reset, a keyboard and contrast check, published on GitHub Pages | `setInterval`, accessibility, Pages |

Publishing on GitHub Pages is a natural ending, because by then the student already knows git and GitHub.

## Chapter 2: Layout

The chapter starts with classes named for the place they are used, then pulls the layout out of them into generic classes that can be combined. It ends with a small layout kit that the student wrote.

### Specific classes first

- **2.1 Centre the front door.** The first class, `.landing`. A flex column that centres the page both ways. This keeps the promise made at the end of lesson 1.1.
- **2.2 The box.** Padding, border, radius and `max-width`. The landing becomes a card.
- **2.3 The top bar.** `.bar` as a flex row with `space-between`: the name on the left, the links on the right.
- **2.4 Cards in a grid.** `.activities` as a grid with `auto-fit` and `minmax`. Resize the window and watch the cards re-flow.

### Then generic classes

- **2.5 Say it once.** `.landing`, `.bar` and `.activities` repeat the same layout lines. Split the layout from the look: `.column`, `.row` and `.grid` do the layout, and the place classes keep only the look.
- **2.6 A scale to pick from.** A spacing scale in `:root` variables, with `.gap-*` and `.padding-*` classes.
- **2.7 Align, justify and width.** `.align-*`, `.justify-*`, a width limit with `.center-self`, and `.width-fill`.
- **2.8 The page shell.** Header, main and footer, with a bar that stays in view using `position: sticky`. This is where `position` is introduced.

The pivot, in one picture:

```text
  before   .landing { display: flex; flex-direction: column; align-items: center; gap: 1rem; }

  after    <main class="landing column gap-l align-center">      .landing keeps only the look
```

### The layout kit

The chapter ends with a `layout.css` of about 25 lines, written by the student. It is modelled on Relayout, the layout CSS used on Codesense's sites: the same ideas and names without the `rl-` prefix.

- `column`: a vertical flex container; the children stretch across.
- `row`: a horizontal flex container; it wraps by default and centres its children up and down.
- `grid`: equal cells with a minimum width, as many on a line as fit.
- `gap-*` and `padding-*`: sizes from the spacing scale, `xs` to `2xl`.
- `align-*` and `justify-*`: where the children sit.
- `width-*` with `center-self`: a width limit, centred in its parent.
- `width-fill`: one child takes the width that is left.

The student writes it rather than loading the real library, so every line is theirs and nothing needs installing. A closing note can say the same idea exists as a real library.

## Next lesson: 2.1 Centre the front door

About 20 minutes. It starts from the end of lesson 1.3: the text sits at the top, centred left to right, with a plain button under it.

1. Add `class="landing"` to `main`. The first class selector: `.landing { }`.
2. Add `display: flex`. The heading, the line and the button jump into a row.
3. Add `flex-direction: column` and they stack again.
4. Add `min-height: 100vh`, `align-items: center` and `justify-content: center`, and everything is centred both ways. Then switch to `row` and watch the two properties swap jobs. An ASCII picture shows the two axes.
5. Add `gap: 1rem`, then check the result in the phone view from lesson 1.2.

New words: class, flex container, main axis and cross axis.

## Open

- Does 2.1 teach classes and flexbox together, as above, or does a tiny classes lesson come first?
- Is the layout kit written by the student, as above, or does the course load the real library?
