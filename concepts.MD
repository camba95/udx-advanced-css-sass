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
