# Cascade Style Sheet - CSS

## Fundamental Pillars for HTML and CSS

### Responsive design

Design that looks good across all screen sizes

- Fluid layouts
- Responsive images
- Media querues
- Correct units
- Desktop-first vs mobile-first

### Maintainable and scalable code

More important for devs than users

- Clean
- Easy to understand
- Feature growth
- Resuable
- How to organize files
- How to name classes
- How to structure HTML

### Web performance

Faster and smallers webs

- Less HTTP requests
- Less code
- Compress code
- Use CSS preprocessor
- Less images
- Compress images

## Cascade

Process of combining different stylesheets and resolving conflicts when more than one rule applies to a certain element.

- Importance

  - User `!important` declarations
  - Author `!important` declarations
  - Author declarations
  - User declarations
  - Default browser declarations

- Specificity: CSS calculates and compares the specificity of the selectors

  - Inline styles
  - IDs
  - Classes, pseudo-classes, attribute
  - Elements, pseudo-elements

- Source order: the last declaration in the code will be applied

**Note:** Specificity is a counting of the categories shown above (`inline`, `IDs`, `classes`, `elements`)

**Note:** Some other good practices for maintainable code:

- `!important` should be used as a last resource, prefer correct use of specificities
- Universal selector `*` has not specificity (0, 0, 0, 0)
- Rely more on `specificity` than on the `order` of selectors
- But, rely on `order` when using 3rd-party stylesheets (put your stylesheet last)

## Value Processing

Following, how units are converted from relative to absolute (`px`), take into account `%` is not an unit yet we include it here.

```css
html,
body {
  font-size: 16px;
  width: 80vw;
}

.header {
  font-size: 150%;
  padding: 2em;
  margin-bottom: 10rem;
  height: 90vh;
  width: 1000px;
}

.header-child {
  font-size: 3em;
  padding: 10%;
}
```

| Unit          | Example                | How to convert                         | Result (`px`)          |
| ------------- | ---------------------- | -------------------------------------- | ---------------------- |
| `%` (font)    | `font-size: 150%`      | `x%` \* parent's computed font-size    | (16 \* 1.5) = 24px     |
| `%` (length)  | `padding: 10%`         | `x%` \* parent's computed width        | (1000 \* 1/10) = 100px |
| `em` (font)   | `font-size: 3em`       | `x` \* parent's computed font-size     | (24 \* 3) = 72px       |
| `em` (length) | `padding: 2em`         | `x` \* current elem computed font-size | (24 \* 2) = 48px       |
| `rem`         | `margin-bottom: 10rem` | `x` \* root computed font-size         | (16 \* 10) = 160px     |
| `vh`          | `height: 90vh`         | `x` \* 1% viewport height              | 90% of viewport height |
| `vw`          | `width: 80vw`          | `x` \* 1% viewport width               | 80% of viewport width  |

**Note:** Some extra information you need to know:

- Each property has an initial value, used if nothing is declared and if there is no inheritance
- Browsers specify a **root font-size** fer each page (usually `16px`)
- Percentages and relative values are always converted to pixels

## Inheritance

- Inheritance passes values for specific properties from parents to children, maintainable code, less to code
- No all properties can be inherited like `margin`, yet font related properties are: `font-family`, `font-size`, `color`, etc.
- The computed value is what gets inherited, not the declared value
- Inheritance only works if someone declares a value for that property, it does not work with initial values
- `inherit` keyword forces inheritance (allowed properties) and `initial` keyword resets a property to its initial value

## Visual Formatting Model

Algorithm that calculates boxes and determines the layout of each of them in the render tree, in order to determine the final layout of the page.

- Dimensions of bozes: box model
- Box type: inline, block
- Positioning scheme: floats and positioning
- Stacking contexts
- Other elements in the render tree
- Viewport size, dimensions of images, etc

### Box Model

Helps define how elements are displayed in the page and how they are sized. Each element in the page can be seen as a rectangle box.

- Content: text, images, etc
- Padding: transparent area around context inside the box
- Border: goes around the padding and content
- Margin: space between boxes
- Fill area: content + padding + border, area affected with backgroung color

The default box model calculates the width and height in the following way:

- **Toltal width:** right border + right padding + specified width + left padding + left border
- **Toltal height:** top border + top padding + specified height + bottom padding + bottom border

A good practice to simplify this is to use `box-sizing: border-box;`, now defined width and height include the padding and border, and also the inner width of the contect area will be reduced to give space to padding and border.

- **Toltal width:** specified width
- **Toltal height:** specified height

### Box Types

Determine how boxes are layout in a page.

- Block-level boxes: defined by `display: block`, but also `flex`, `list-item`, `table` values produces block level boxes

  - Elements formatted as blocks
  - Take 100% of parent's width
  - Line break, vertically aligned
  - Box model from the section before

- Inline boxes: defined by `display: inline`

  - Content distributed in lines
  - Occupies only content's space
  - No line breaks, no heigth, no width (box model)
  - Horizontal paddings and margins only (box model)

- Inline-block boxes: defined by `display: inline-block`
  - A mix of block and inline
  - Occupies only content's space (inline)
  - No line breaks (inline)
  - Box model from the section before (block)

### Positioning Schemes

- Normal flow

  - Default positioning scheme (default or `position: relative`)
  - Not floated, not absolutele positioned
  - Elements are laid out according to the order in the code

- Floats: `float: left` or `float: right`

  - Elements is removed from the normal flow
  - Text and inline elements wrap around floated elements
  - The continer will not adjust its height to floated element

- Adsolute positioning
  - Elements is removed from the normal flow
  - No impact or surrounding elements
  - Use `top`, `bottom`, `left`, `right` to offset the element from its relatively positioned container
  - Absolute positioned elements overlap other elements

### Stacking Contexts

Solves the problem of overlaped elements occuping the same space. Determines in which order elements are rendered in the page, `z-index` is the most widely known property that creates stacking contexts (there are others) and it works with `relative` and `absolute` positions.

## CSS Architecture

### Think - Component Driven Design

Think of the page in terms of modular components.

- Components are the building blocks to construct interfaces.
- They should be reusable and independent (even from parent element)

### Build - BEM

Block Element Modifier, strategy for naming CSS classes, `.block__element--modifier {}`

- Block: standalone component that is meaningful on its own (`recipe`, `header`, `btn`)
- Element: part of a block that has no standalone meaning (`recipe__hero`, `header__title`)
- Modifier: a different version of a block or element (`btn--round`, `recipe__hero--large`, `recipe__hero--small`)

### Architect - 7-1 Pattern

7 different folders for partial Sass files and 1 main Sass file to import all of the other files into a compiled CSS stylesheet. These folders are: base, components, layout, pages, themes, abstracts, vendors.
