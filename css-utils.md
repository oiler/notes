## snippets

```css
/* responsive media */
img, video, audio { max-width:100%; height:auto; }
/* text selection */
::selection { color:#000; background:#fbd404; }
/* clearfix floats */
.clearfix::after { content:''; display:table; clear:both; }
/* box sizing */
html { box-sizing:border-box; } 
*, *::before, *::after { box-sizing:inherit; }
/* respect reduced motion */
@media (prefers-reduced-motion: reduce) {
  * { animation:none !important; transition:none !important; }
}
/* box shadow material design */
.classname { box-shadow:0 10px 20px rgba(0, 0, 0, 0.19), 0 6px 6px rgba(0, 0, 0, 0.23); }
/* color inherit */
a { color:inherit; }
```

## guides

* [snippets](https://justmarkup.com/log/2018/03/collection-of-css-snippets/)
* [centering](https://css-tricks.com/centering-css-complete-guide/)
* [normalize](https://github.com/necolas/normalize.css/blob/master/normalize.css)
