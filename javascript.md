# Javascript

## High Level 
* Favor _composition_ over _inheritance_
** design types around what they do, not what they are
** use *can-do*, *has-a*, or *uses-a* relationships instead of *is-a* relationships.
** "new and this are some kind of unintuitive weird clown rainbow trap that you trip over all the time."[source](https://www.youtube.com/watch?v=ImwrezYhw4w)


## Object methods

```
var pizza = { 
    "toppings"  : ["mushrooms", "meatballs"],
    "sauce"     : "light",
    "cheese"    : "extra"
};
var dough = { "type": "thin crust" };
```

[assign][](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)
```
var lunchOrder = Object.assign({}, pizza, dough);
console.log(lunchOrder);
// { toppings: [ 'mushrooms', 'meatballs' ], sauce: 'light', cheese: 'extra', type: 'thin crust' }
```
[keys](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/keys)
console.log(Object.keys(pizza)); 
// returns: [ 'toppings', 'sauce', 'cheese' ]
console.log(Object.keys(pizza.toppings)); 
// returns: [ '0', '1' ]
Object.keys(pizza.toppings).forEach(function(key) {
    console.log(key, pizza.toppings[key]);
});
// returns: 0 mushrooms \n 1 meatballs
```

## Examples of composition
object _composition_ with [Object.assign()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)

```
const barker = (state) => ({
    bark: () => console.log('Woof, I am ' + state.name)
})

const driver = (state) => ({
    drive: () => state.position = state.position + state.speed
})

barker({name: 'karo'}).bark()
// woof, i am karo

const murderRobotDog = (name) => {
    let state = {
        name,
        speed: 100,
        position: 0
    }
    return Object.assign
        {},
        barker(state),
        driver(state),
        killer(state)
    }
}
murderRobotDog('sniffles').bark()
// woof, i am sniffles
```

_factories_
are functions that create objects, to use instead of classes
es5
```
var pizza = function pizza() {
    var toppings = 'mushrooms, meatballs';
    return {
        cook: function cook() {
            console.log(toppings);
        }
    }
}
var myPizza = pizza();
myPizza.cook();
```
es6
```
const pizza = () => {
    const toppings = 'mushrooms, meatballs';
    return {
        cook: () => console.log(toppings)
    }
}
const myPizza = pizza();
myPizza.cook();
```

## Manipulating arrays

_[filter](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)_,
_[map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)_,
_[reduce](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)_ methods
```
var pizza = {};
var toppings = ["mushrooms","meatballs"];

// filter: create new array with all elements that **pass the test** implemented by the provided function.
function addToppings(elem, index, array) {
  if (typeof elem === "string") {
        return elem;
    }
}

// reduce: simplify to a **single value** by running function on each in original (from left-to-right)
function listToppings(previousValue, currentValue, currentIndex, array) {
  return previousValue + ' ' + currentValue;
}

// map: create new array by calling a function on **all** elements in original
function doubleMeat(currentValue, index, array) {
    if (currentValue === "meatballs") {
        return 'double ' + currentValue;
    } else {
        return currentValue;
    }
}

pizza.filtered = toppings.filter(addToppings);
pizza.reduced = toppings.reduce(listToppings);
pizza.mapped = toppings.map(doubleMeat);
console.log(pizza);
// returns: 
{ filtered: [ 'mushrooms', 'meatballs' ],
  reduced: 'mushrooms meatballs',
  mapped: [ 'mushrooms', 'double meatballs' ] }
```
[more1](https://danmartensen.svbtle.com/javascripts-map-reduce-and-filter)
[more2](http://www.macwright.org/2015/01/03/reduce-juice.html)


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
var pizza = function pizza(toppings) {
    var pizzaWithToppings = '';
    toppings.forEach( function addTo(item) {
        pizzaWithToppings += item + ' ';
    });
    return pizzaWithToppings;
};
console.log(pizza(["mushrooms", "onions", "peppers"]));
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
* [Video - Philip Roberts JSConf 2014](https://www.youtube.com/watch?v=8aGhZQkoFbQ)
* [Live - visualize event loop](http://latentflip.com/loupe)
* [Dev Tools - JS debugging via Chrome DevTools Sources panel](https://developer.chrome.com/devtools/docs/javascript-debugging)
* [Dev Tools - How to Step Through the Code](https://developers.google.com/web/tools/chrome-devtools/debug/breakpoints/step-code?hl=en)






##  [Strict Mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode)

[Differences from non-strict to strict](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode/Transitioning_to_strict_mode)
* Syntax errors
* New runtime errors
* Semantic differences

1. strict mode eliminates some JavaScript silent errors by changing them to throw errors. 
2. strict mode fixes mistakes that make it difficult for JavaScript engines to perform optimizations: strict mode code can sometimes be made to run faster than identical code that's not strict mode. 
3. strict mode prohibits some syntax likely to be defined in future versions of ECMAScript.





## ES6

[_arrow functions_](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
give shorter function syntax, allowing for smaller inline single purpose functions
parentheses are optional if only one parameter

```
"use strict";
function addToppings(toppings) {
    let pizzaWithToppings = '';
    toppings.forEach( function addTo(item) {
        pizzaWithToppings += item + ' ';
    });
    return pizzaWithToppings;
}

// traditional
var pizza = function pizza(toppings) {
    return addToppings(toppings);
};

// arrow
const pizzaa = (toppings) => addToppings(toppings);

console.log('reglr:', pizza(["mushrooms", "onions", "peppers"]));
console.log('arrow:', pizzaa(["mushrooms", "onions", "peppers"]));
```


binary floating point

http://rainsoft.io/how-three-dots-changed-javascript/