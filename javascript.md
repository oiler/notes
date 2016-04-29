# Javascript


## Functions
"Wherever possible, make sure that your functions don’t change anything outside the function itself. Return amended copies rather than originals."

_function declaration_
```
function pizza() {
    // code
}
```

_function expression_
```
var pizza = function() {
    // code
};
```


##  [Strict Mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode)

[Differences from non-strict to strict](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode/Transitioning_to_strict_mode)
* Syntax errors
* New runtime errors
* Semantic differences

1. strict mode eliminates some JavaScript silent errors by changing them to throw errors. 
2. strict mode fixes mistakes that make it difficult for JavaScript engines to perform optimizations: strict mode code can sometimes be made to run faster than identical code that's not strict mode. 
3. strict mode prohibits some syntax likely to be defined in future versions of ECMAScript.




