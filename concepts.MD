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

### Cascade

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
