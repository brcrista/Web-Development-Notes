# HTML & CSS book

Random reading notes from the book.
I've heard or sort-of know a lot of these things, but I'm going to write them down anyway since this served as a refresher.

## Box model
- **Border** is exactly what it sounds like
- **Padding** is between the content and the border
- **Margin** is outside of the border
- Margins **collapse** when two elements' margins touch. This means that only the larger margin is used.

## Basic Layout
- **Normal flow** (the default) just puts each block element beneath the previous one
- **Relative positioning** moves an element relative to its position in the normal flow. Normal flow resumes after that element.
- **Absolute positioning** moves an element relative to its parent. Other elements are not affected.
- **Fixed positioning** puts an element in the same place in the browser's window, even when you scroll.
- **Floating** puts elements one after another horizontally.
  - You can **clear** the float to start a new "row."
  - If a container has all floating elements inside it, it will have 0 height. You can fix this with

```css
div {
    overflow: auto;
    width: 100%;
}
``` 

Modern websites need a flexible, or **liquid**, layout to handle differently sized screens and font sizes. With this, widths and heights need to be expressed as percentages instead of absolute values.

### Grids
A **grid system** is often helpful in laying out content. Grid systems are usually handled by **CSS frameworks** such as Boostrap (though CSS 3 now has grids built in.) A grid is defined by a number of columns. Each element then takes up some number of columns.

A common design is to have a heading, content, and footer. In the content, there is a feature (full width), then smaller elements underneath.

An old way to make grids in a **fixed layout** (where all widths are some static number of pixels) was to float a bunch of divs and compute the widths of the divs and their parent so they fall into a grid. Of course, the grid doesn't hold together for liquid layouts. Frameworks fix this problem because they will adapt the grid based on the size of the viewport.

### Centering content
We have three ways now to center content:
1. Set `text-align: center` on the parent element
2. Set `display: block` (if needed) and `auto` for the left and right margins
3. Use a grid system

## Images
If you are using a pattern (called a **texture** or a **wallpaper**) for a background image, you can simply make the image a small tile and it will be repeated to make the background by default.

A **sprite** is a single image used for several parts of an interface. A common example is having a button sprite that contains all the states of a button. You could make a different image for each state, but this increases the number of requests the browser has to make. Instead, you can just concatenate the images and selectively show the part of the image that pertains to the current state.

## HTML 5

HTML 5 adds some new elements that are more descriptive replacements for `div` in some places. Here are some examples:

- `header`
- `footer`
- `nav` (usually contained in `header`)
- `article`
- `aside`
- `section`
- `figure`

HTML 5 also lets you wrap a block element with `<a>`, which was not allowed before.

## Design

Step 1: User profiles, what are we doing, normal business-plan type of stuff.


Step 2: A **sitemap** organizes the content that needs to go on a site.

Step 3: A **wireframe** is a mock-up of the content on a page and its layout. It ignores things like font, color, or images. It might be done in software like Photoshop or Illustrator or even just sketched on paper.

A wireframe establishes that function is correct before moving on to design. If you show a stakeholder a real design, they'll often get sidetracked by the visuals.

The purpose of design is to **communicate**.
There are three principles of design:
1. Visual hierarchy
2. Grouping
3. Similarity

**Visual hierarchy** means prioritizing information and making the most important information the most prominent. Having a masthead, logo, and screenshot at the top of a page is an example of visual hierarchy. Larger size, color, and unique style are ways to declare a visual hierarchy.

**Grouping** means putting related information close to each other. It helps people organize the information in their minds without really reading it.

**Similarity** is other dimension of organization along with grouping. Related content or function should look similar.

### Nav bar
* Keep the nav bar to 8 items, max. (Cf. *Code Complete*'s advice on variables in a scope.)
* The nav bar should reflect the site **structure**. Keep functionality such as login and search out of it.
* For long pages, add secondary navigation in a sidebar.
* Keep the nav bar the same on every page.
* The nav bar should show which page you are on currently.
