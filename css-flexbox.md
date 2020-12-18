# CSS Flexbox

## Resources

- <https://flexboxfroggy.com>
- <https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Basic_Concepts_of_Flexbox>
- <https://www.w3schools.com/csS/css3_flexbox.asp>

## Flex Containers

Set `display: flex` on an element to make it a **flex container**:

```css
.flex-container {
    display: flex;
}
```

## Flexbox Properties

These additional properties go on the flex container:

`justify-content`; alignment along the primary axis (horizontal by default; see `flex-direction`)
- `flex-start` (default)
- `flex-end`
- `center`
- `space-between`
- `space-around`

`align-items`: alignment along the secondary axis (vertical by default)
- `flex-start`
- `flex-end`
- `center`
- `baseline`
- `stretch` (default)

`align-content`: spacing of rows
- `flex-start`
- `flex-end`
- `center`
- `space-between`
- `space-around`
- `stretch` (default)

`flex-direction`: axis and ordering
- `row` (default)
- `row-reverse`
- `column`
- `column-reverse`

`align-self`: per-element alignment
- same as `align-items`

`order`: per-element ordering. Elements are ordered in the flexbox by ascending integer value.
- `0` (default)

`flex-wrap`: whether elements are forced into a single row or can spread over multiple rows.
- `nowrap` (default)
- `wrap`
- `wrap-reverse`

`flex-flow`: `flex-direction` and `flex-wrap` combined
- `<flex-direction> <flex-wrap>`
