
## Vanilla JS click tracking

Usage:

```html
<a target="_blank"
    rel="noopener"
    data-event="link"
    data-ga_category="your_category"
    data-ga_action="your_action"
    data-ga_label="your_label"
    href="https://twitter.com/">twitter.com</a>
```

```javascript
<script>
    ;(function (window, document, undefined) {
        'use strict';
        var events = document.querySelectorAll('[data-event]');
        function ga_assign(name, event) {
            if (typeof name !== 'string') {
                return;
            }
            var category, action, label;
            var attrs = {
                "category": "category",
                "action": "action",
                "label": "label"
            }
            var defaults = {
                "category": "mycat1",
                "action": "myaction1",
                "label": "mylabel1"
            }
            var output = '';
            var attr = 'data-ga_' + attrs[name];

            if ( typeof event.attributes[attr] !== 'object' ) {
                output = defaults[name];
            } else {
                output = event.attributes[attr].nodeValue;
            }
            return output;
        }

        Object.keys(events).forEach(function(key) {
            var event = events[key];
            var ga_category = ga_assign('category', event);
            var ga_action = ga_assign('action', event);
            var ga_label = ga_assign('label', event);
            event.addEventListener("click", function (event) {
                ga(
                    'send',
                    'event',
                    ga_category,
                    ga_action,
                    ga_label,
                    {nonInteraction: false}
                );
                //console.log( 'click', ga_category, ga_action, ga_label );
            });
        });
    })(window, document);
</script>
```