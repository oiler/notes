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

_method literals_
* are function expressions assigned to object literals
* group related functions together, for better organization
```
var pizza = {
    dough: function() {},
    toppings: function() {}
};
```

_named function expression_
```
var pizza = function pizza() {
    // code
};
```

_lambdas_
```
var pizza = function pizza() {
    var toppings = '';
    ["mushrooms", "onions", "peppers"].forEach( function addTo(item) {
        toppings += ' '+item;
    });
    return toppings;
};
```

_immediately invoked function expressions_
```
(function() {
    // pizza code
}());
```

[_bind()_](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)
```
cook. = pizza.cook.bind(pizza);

```

_closures_
store function state, even after the function has returned
```
var cook = function cook() {
    var toppings = ['mushrooms', 'onions', 'peppers'];
    var addToppings;
    addToppings = function addToppings() {
        return toppings;
    }
    return { 
        addToppings: addToppings
    };
};

var pizza = cook();
console.log( pizza.addToppings() );
```

_arity_ & _extend_
is the number of variables that are passed as parameters in function
```
function cookPizza( toppings, cheese, sauce, dough, cut ); // arity = 5
```
better way to do this is pass params as objects (need _extend_ method API in lib)
```
function cookPizza(options) {
    return $.extend({}, newPizza, options);
}
var newPizza = cookPizza({
    toppings: ['mushrooms', 'onions', 'peppers'],
    cheese: 'extra',
    sauce: 'regular',
    dough: 'pan',
    cut: 'normal'
});
```

_polymorphism_ & [_slice_](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)
behave differently based on the parameters you pass into them
```
function cookPizza(options) {
    var args = [].slice.call(arguments, 0); // is same as Array.prototype.slice.call(arguments, 0);
    var toppings,
        quantity
    ;
    if( typeof options === 'string' ) {
        toppings = options;
        args.shift();
    }
    return('I need ' + args + ' pizzas with ' + toppings + ' on them!');
}
var pizza = cookPizza( 'mushrooms', 2 );
// would need better typeof / shift logic if we wanted to do more with args, such as flip the order or add more
var pizza2 = cookPizza( 2, 'mushrooms' ); // "I need 2,mushrooms pizzas with undefined on them!"
```

_fuild method chaining_
what jquery and d3 do
```
$('.myDivClass').hide().css('color','black').show();
```




## [Event Loop](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop)
JS is single threaded, features a call stack and queue  
when something is running in call stack, browser can't do anything else  
solution is async callbacks  
concurrency & the event loop  
browser is more than just runtime  
for example, setTimeout is api provided by the browser  
    move from the stack to the webapi into task queue  
event loop pulls from queue and pushes into stack, if stack is clear

_more_
* [Visualize event loop](http://latentflip.com/loupe)
* [JS debugging via Chrome DevTools Sources panel](https://developer.chrome.com/devtools/docs/javascript-debugging)
* [How to Step Through the Code](https://developers.google.com/web/tools/chrome-devtools/debug/breakpoints/step-code?hl=en)






##  [Strict Mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode)

[Differences from non-strict to strict](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode/Transitioning_to_strict_mode)
* Syntax errors
* New runtime errors
* Semantic differences

1. strict mode eliminates some JavaScript silent errors by changing them to throw errors. 
2. strict mode fixes mistakes that make it difficult for JavaScript engines to perform optimizations: strict mode code can sometimes be made to run faster than identical code that's not strict mode. 
3. strict mode prohibits some syntax likely to be defined in future versions of ECMAScript.




