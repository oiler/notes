## Plugin Best Practices

* use conditional loading (use is_single, is_page, etc)
* avoid naming collisions (namespace functions, classes, hooks, global variables) with `isset()` `function_exists()` `class_exists()` `defined()`
* use OOP where appropriate




## Plugin Templates and Examples

* (single file, functions)[https://github.com/GaryJones/move-floating-social-bar-in-genesis/blob/master/move-floating-social-bar-in-genesis.php]
* (single file, class)[https://github.com/norcross/wp-comment-notes/blob/master/wp-comment-notes.php]
* (multiple files)[https://github.com/DevinVinson/WordPress-Plugin-Boilerplate]
* (boilerplate)[https://github.com/claudiosanches/wordpress-plugin-boilerplate]
* (skeleton)[https://github.com/ptahdunbar/wp-skeleton-plugin]
* (slash architecture)[https://jjj.blog/2012/12/slash-architecture-my-approach-to-building-wordpress-plugins/]
* (mvc slides)[https://iandunn.name/content/presentations/wp-oop-mvc/mvc.php/]
* (mvc template)[https://wordpress.org/plugins/wp-mvc]


## Other Links
* (plugin APIs directory)(https://codex.wordpress.org/WordPress_API%27s)
* (plugin API Filters reference)[https://codex.wordpress.org/Plugin_API/Filter_Reference]
* (pluggable functions directory)[https://codex.wordpress.org/Pluggable_Functions]
* (functions reference directory)[https://developer.wordpress.org/reference/functions/]
* (readme validator)[https://wordpress.org/plugins/developers/readme-validator]

## Code Snippets

prevent php files from being called directly
```php
if (!defined('ABSPATH')) {
    exit;
}
```

include file
```php
if (is_admin()) }
    requre_once plugin_dir_path( __FILE__) . 'relative-path-file.php';
}
```