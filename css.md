# CSS 

## new features
https://caniuse.com/

### filter


### calc
```
width: -webkit-calc(100% / 3 - 100px + 20px * 1);
.col-1 { width: calc(100% / 12 * 1); }
.col-4 { width: calc(100% / 12 * 4); }
```

### grid
[mdn](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout)


### flexbox

links
======
* [mdn docs](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout)
* [css tricks guide](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
* [flexbox demo sandbox](https://codepen.io/oiler/pen/jQowRw)

notes
======
**flex container**
------------------
```css
display: flex | inline-flex;
flex-direction: row | row-reverse | column | column-reverse;
flex-wrap: nowrap | wrap | wrap-reverse;
```
`flex-flow: <‘flex-direction’> || <‘flex-wrap’>`
* shorthand of flex-direction and flex-wrap 
* default=row nowrap)

`justify-content: flex-start | flex-end | center | space-between | space-around | space-evenly;`
* defines the alignment along the main axis

`align-items: flex-start | flex-end | center | baseline | stretch;`
* defines the default behavior for how flex items are laid out along the cross axis

`align-content: flex-start | flex-end | center | space-between | space-around | stretch;`
* aligns a flex container's lines within when there is extra space in the cross-axis


**flex items**
------------------
```css
order: <integer>; /* default is 0 */
flex-grow: <number>; /* default 0 */
flex-shrink: <number>; /* default 1 */
flex-basis: <length> | auto; /* default auto */ 
```
`flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]`
* shorthand for flex-grow, flex-shrink and flex-basis
* recommended use over individual properties

`align-self: auto | flex-start | flex-end | center | baseline | stretch;`


### columns
[css tricks](https://css-tricks.com/guide-responsive-friendly-css-columns/)
```
column-count: auto | <integer> | inherit | initial | unset;
column-gap: normal | <integer> | inherit | initial | unset;
column-rule: <'column-rule-width'> || <'column-rule-style'> || <'column-rule-color'>
column-width: auto | <integer> | inherit | initial | unset;
column-span: none | all;
```

### pseudo classes
* :active
* :any
* :any-link
* :checked
* :default
* :dir()
* :disabled
* :empty
* :enabled
* :first
* :first-child
* :first-of-type
* :fullscreen
* :focus
* :hover
* :indeterminate
* :in-range
* :invalid
* :lang()
* :last-child
* :last-of-type
* :left
* :link
* :not()
* :nth-child()
* :nth-last-child()
* :nth-last-of-type()
* :nth-of-type()

### viewport units
[css tricks](https://css-tricks.com/fun-viewport-units/)
* Viewport Width (vw)
* Viewport Height (vh) 
* Viewport Minimum (vmin) 
* Viewport Maximum (vmax)

### email client isolation
```css
.★:not(#★){ /* for targeting AOL */} 
@media yahoo{/* for targeting Yahoo */} 
u+ .body .foo{/* for targeting Gmail */} 
#MessageWebViewDiv .foo{/* for targeting Samsung mail */} 
[OWA] .foo{/* for targeting http://Outlook.com  */}
```