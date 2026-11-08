# Flexbox and grid cheatsheet

The two CSS tools for arranging things on a page. **Flexbox** puts the children of a tag in one line, a row or a column. **Grid** puts them in rows and columns together.

## Sizes used here

| Unit | What it is |
|---|---|
| `rem` | a multiple of the browser's text size. `1rem` is 16 pixels at the normal setting, so `14rem` is 224 pixels |
| `fr` | one share of the free space in a grid. In a grid 600 pixels wide, `1fr 2fr` makes columns of 200 and 400 pixels, and `14rem 1fr` makes columns of 224 and 376 pixels |
| `vh` | one percent of the height of the window. `100vh` is the whole height |

## Which one?

| You want | Use |
|---|---|
| things side by side, or one under the other | flexbox |
| a bar with a name on the left and links on the right | flexbox |
| one thing in the middle of the window | flexbox, or grid |
| cards in as many columns as fit | grid |
| things that line up in rows and columns | grid |
| a page with a header, a main part and a footer | grid |

In short: one direction is flexbox, and two directions is grid. They work together. A grid of cards can have a flexbox column inside each card.

## Container and items

Both start with a **container**, the tag that holds the others. The tags directly inside it are its **items**.

```
  <div class="container">      the container
      <div>item</div>          the items
      <div>item</div>
      <div>item</div>
  </div>
```

The container gets `display: flex` or `display: grid`. Most other properties go on the container too, and arrange all of its items. A few go on one item, to give it its own place or size.

## Flexbox

### The two axes

```
  flex-direction: row

  +-----+ +-----+ +-----+
  |  1  | |  2  | |  3  |      main axis: left to right
  +-----+ +-----+ +-----+      cross axis: up and down

  flex-direction: column

  +-----+
  |  1  |
  +-----+                      main axis: top to bottom
  +-----+                      cross axis: left and right
  |  2  |
  +-----+
```

`justify-content` works along the main axis, and `align-items` works along the cross axis. They swap jobs when the direction changes.

### On the container

| Write | What it does |
|---|---|
| `display: flex;` | the tag is a flex container: its children go in a row |
| `flex-direction: row;` | the main axis goes left to right. This is the default |
| `flex-direction: column;` | the main axis goes top to bottom |
| `justify-content: center;` | where the children sit along the main axis |
| `align-items: center;` | where the children sit across it |
| `gap: 1rem;` | the space between the children, and not around the outside |
| `flex-wrap: wrap;` | the children move to a new line when there is no room |

### `justify-content`: along the main axis

Three items in a row. Each dot is free space:

```
  flex-start       [1][2][3]...........................
  center           .............[1][2][3]..............
  flex-end         ...........................[1][2][3]
  space-between    [1].............[2]..............[3]
  space-around     ....[1].........[2].........[3].....
  space-evenly     .......[1].......[2].......[3]......
```

`flex-start` is the default. `space-between` puts the first child at the start and the last at the end, and shares the space that is left between them. `space-around` and `space-evenly` share the space too, and leave room at the two ends.

### `align-items`: across

| Value | In a row | In a column |
|---|---|---|
| `stretch` | the children are as tall as the row. This is the default | the children are as wide as the column |
| `flex-start` | at the top | at the left |
| `center` | in the middle, up and down | in the middle, left and right |
| `flex-end` | at the bottom | at the right |

`stretch` is why a button in a column spreads across the whole width until you set `align-items`.

### On an item

| Write | What it does |
|---|---|
| `flex: 1;` | this child takes all the space that is left in the line |
| `align-self: flex-end;` | this child places itself across the line, as `align-items` would |
| `margin-left: auto;` | this child, and the ones after it, are pushed to the end of the row |

### Patterns

Centre one thing in the window:

```css
.centre {
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
}
```

A bar with a name on the left and links on the right:

```css
.bar {
    display: flex;
    justify-content: space-between;
    align-items: center;
}
```

A column with space between the items:

```css
.stack {
    display: flex;
    flex-direction: column;
    gap: 1rem;
}
```

A row where one child fills the space that is left. Give the item `flex: 1`:

```css
.row {
    display: flex;
    gap: 1rem;
}

.row .grow {
    flex: 1;
}
```

A row that moves to a new line when it is full:

```css
.chips {
    display: flex;
    flex-wrap: wrap;
    gap: 0.5rem;
}
```

The last item pushed to the end, such as a Delete button:

```css
.row .last {
    margin-left: auto;
}
```

## Grid

### On the container

| Write | What it does |
|---|---|
| `display: grid;` | the tag is a grid: its children go in rows and columns |
| `grid-template-columns: repeat(3, 1fr);` | three columns of the same width |
| `grid-template-columns: repeat(auto-fit, minmax(14rem, 1fr));` | as many columns as fit, none narrower than 14rem |
| `grid-template-columns: 14rem 1fr;` | a column of 14rem, and a column that takes the rest |
| `grid-template-columns: 1fr 2fr;` | two columns, the second twice as wide |
| `gap: 1rem;` | the space between the cells |
| `gap: 0.5rem 2rem;` | the space between rows, then the space between columns |
| `grid-auto-rows: minmax(5rem, auto);` | every row is at least 5rem tall, and grows with its content |
| `place-items: center;` | every item in the middle of its cell, both ways |

### Sizes of columns

`repeat` and `minmax` each take two arguments, the two things inside their brackets:

```
  repeat( 3 , 1fr )                  how many times, then what to repeat
  repeat( auto-fit , 14rem )         as many times as fit, then what to repeat
  minmax( 14rem , 1fr )              the smallest size, then the largest
```

| Write | What it means |
|---|---|
| `1fr` | one share of the free space |
| `repeat(3, 1fr)` | three columns, each one share |
| `minmax(14rem, 1fr)` | a size with a smallest and a largest value: never narrower than 14rem, never wider than its share |
| `auto-fit` | as many columns as fit. With few items, empty columns disappear and the items stretch |
| `auto-fill` | as many columns as fit. With few items, the empty columns stay, so the items keep a normal size |
| `14rem` | a fixed width |

How `repeat(auto-fit, minmax(14rem, 1fr))` works, in a grid 852 pixels wide with a gap of 1rem:

```
  4 columns of 14rem need 896 + 48 = 944 pixels     too wide
  3 columns of 14rem need 672 + 32 = 704 pixels     they fit
  852 - 704 = 148 pixels are left, shared by 3      each column is 273 pixels
```

### Where an item sits in its cell

In a grid these do not depend on a direction: `justify` is always left and right, and `align` is always up and down.

| Write | What it does |
|---|---|
| `justify-items: center;` | every item in the middle of its cell, left to right |
| `align-items: center;` | every item in the middle of its cell, up and down |
| `justify-self: end;` | one item at the right of its cell |
| `align-self: end;` | one item at the bottom of its cell |

### On an item

| Write | What it does |
|---|---|
| `grid-column: span 2;` | this item takes two columns |
| `grid-row: span 2;` | this item takes two rows |
| `grid-column: 1 / -1;` | this item takes the whole row, from the first column line to the last |

### Patterns

Cards that re-flow when the window changes size:

```css
.cards {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(14rem, 1fr));
    gap: 1rem;
}
```

Columns at least 18rem wide: as many as fit on a wide window, and one on a phone:

```css
.columns {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(18rem, 1fr));
    gap: 1rem;
}
```

A sidebar and a main part:

```css
.page {
    display: grid;
    grid-template-columns: 14rem 1fr;
    gap: 1rem;
}
```

One thing in the middle of the window:

```css
.centre {
    display: grid;
    place-items: center;
    min-height: 100vh;
}
```

A header, a main part and a footer, with the footer at the bottom of the window even when the main part is short:

```css
.shell {
    display: grid;
    grid-template-rows: auto 1fr auto;
    min-height: 100vh;
}
```

One item as wide as the whole grid, such as a heading above the cards:

```css
.cards .wide {
    grid-column: 1 / -1;
}
```

## Layout classes in the Student Planner

These are some of the classes in the Student Planner's `layout.css`. Each one is one or two of the lines above, with a name. The [CSS cheatsheet](03-css-cheatsheet.md) has the full set, with the spacing and width classes.

| Class | The CSS it stands for |
|---|---|
| `column` | `display: flex; flex-direction: column;` |
| `row` | `display: flex;` |
| `grid` | `display: grid; grid-template-columns: repeat(auto-fit, minmax(14rem, 1fr));` |
| `justify-between` | `justify-content: space-between;` |
| `justify-center` | `justify-content: center;` |
| `align-center` | `align-items: center;` |
| `width-fill` | `flex: 1;` |
| `gap-md` | `gap: var(--space-md);` |

## Stuck?

- **Nothing moves.** The property is on the child. Put it on the container, the tag that holds the others, and check that the container has `display: flex` or `display: grid`.
- **`justify-content` does nothing.** The container is already as big as its children along the main axis, so there is no room to move in. In a column, give it a height, such as `min-height: 100vh`. On a grid whose columns are `1fr`, the columns already fill the whole width, so `justify-content`, and the classes `justify-between` and `justify-center`, have nothing left to share.
- **`align-items: center` goes the wrong way.** It works across the main axis. In a row that is up and down, and in a column it is left and right.
- **`gap` does nothing.** The tag is not a flex container or a grid. `gap` is the space between the children of one.
- **`flex: 1` does nothing.** Its parent is not a flex container. In a column, the parent also needs a height to share. A column is only as tall as its children, so there is no space left for `flex: 1` to take until you give the column a height, such as `min-height: 100vh`. The same goes for the `width-fill` class.
- **A row runs off the page.** Add `flex-wrap: wrap` to the container, or use a grid with `repeat(auto-fit, minmax(14rem, 1fr))`.
- **The cards are stretched when there are only two.** That is `auto-fit` sharing the room. Use `auto-fill` to keep their size.
