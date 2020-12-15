# WordPress Guide

## Page Conditionals
https://codex.wordpress.org/Conditional_Tags

* home page

```
if ( is_front_page() && is_home() ) {
  // Default homepage
} elseif ( is_front_page() ) {
  // static homepage
} elseif ( is_home() ) {
  // blog page
} else {
  //everything else
}
```

* is_single()
* is_page()
* is_category( '9' ) 
* is_page_template( 'about.php' )
* is_tag() 
* is_search() 
* is_archive() 

---

## Images

* ### Setup functions.php
```php
// add post thumbnail support
add_theme_support( 'post-thumbnails' );

// theme custom image sizes
add_theme_support( "theme-custom" );
add_image_size( "theme-custom", 360, 215, true );

// add theme custom images sizes to block dropdown
if ( !function_exists( "theme_custom_image_sizes" ) ) :
function theme_custom_image_sizes( $sizes ) {
    return array_merge( $sizes, array(
            "theme-custom" => __( "Theme Custom" ),
        )
    );
}
endif;
add_filter( 'image_size_names_choose','theme_custom_image_sizes' );
```

* ### Core Default Sizes
| Name | Max-Width | Max-Height |
| --- | --- | --- |
| full | (original) | (original) |
| medium_large | 768 | (scaled) |
| 1536x1536 | 1536 | 1536 |
| 2048x2048 | 2048 | 2048 |
* For example, a 3000x2000 image will produce: 768x512, 1536x1024, 2048x1365
* And a 2000x3000 portrait image will produce: 768x1152, 1024x1536, 1365x2048
* [WP v5.3 added](https://make.wordpress.org/core/2019/10/09/introducing-handling-of-big-images-in-wordpress-5-3/) "big image" scaling sizes 1536 and 2048

* ### Admin Default Sizes
| Name | Max-Width | Max-Height |
| --- | --- | --- |
| Thumbnail | 150 | 150 |
| Medium | 300 | 300 |
| Large | 1024 | 1024 |
* These settings are customized in WP Admin
* The Thumbnail WP default will force crop (this setting can be disabled)
* The Medium and Large sizes will scale, and not crop, image uploads 
* For example, a 3000x2000 image will produce: 300x300, 600x400, and 1024x683
* And a 2000x3000 portrait image will produce: 300x300, 400x600, 683x1024

* ### Plugin Image Sizes - Atomic Blocks
| Name | Width | Height | Crop | Ratio |
| --- | --- | --- | --- | --- |
| ab-block-post-grid-landscape | 600 | 400 | true | 1.5 |
| ab-block-post-grid-square | 600 | 600 | true | 1.0 |
* Both of these plugin images will force crop

---

## Other Important Links
* (plugin APIs directory)(https://codex.wordpress.org/WordPress_API%27s)
* (plugin API Filters reference)[https://codex.wordpress.org/Plugin_API/Filter_Reference]
* (pluggable functions directory)[https://codex.wordpress.org/Pluggable_Functions]
* (functions reference directory)[https://developer.wordpress.org/reference/functions/]
* (readme validator)[https://wordpress.org/plugins/developers/readme-validator]
* (shortcode attrs)[https://developer.wordpress.org/reference/functions/shortcode_atts/]
* (dashicons)[https://developer.wordpress.org/resource/dashicons/#id-alt]

---
## Post Revisions

* delete old revisions, via cli

`wp post delete $(wp post list --post_type='revision' --format=ids)`

* delete old revisions, via sql

`DELETE FROM wp_posts WHERE post_type = “revision”;`

* limit number of allowed revisions, via wp-config

`define('WP_POST_REVISIONS', 3);`

* turn off revisions

`define('WP_POST_REVISIONS', false);`

---

## Code Snippets

* ### parse args
```php
//https://developer.wordpress.org/reference/classes/wp_query/parse_query/
$args = array(
  'numberposts' => 10,
  'post_type'   => 'book'
);
$latest_books = get_posts( $args );

```

* ### security - prevent php files from being called directly
```php
if (!defined('ABSPATH')) {
    exit;
}
```

* ### include file
```php
if (is_admin()) }
    requre_once plugin_dir_path( __FILE__) . 'relative-path-file.php';
}
```

* ### add admin menu item
```php
function myplugin_add_toplevel_menu() {
    add_menu_page( //use add_submenu_page for submenu
        'MyPlugin Settings', //string $page_title, 
        'MyPlugin', //string $menu_title, 
        'manage_options', //string $capability, 
        'myplugin', //string $menu_slug, 
        'myplugin_display_settings_page', //callable $function = '', 
        'dashicons-admin-generic', //string $icon_url = '',
        null //$position = null 
    );
}
add_action( 'admin_menu', 'myplugin_add_toplevel_menu' );
```

* ### admin display settings callback
```php
function myplugin_display_settings_page() {
    if ( ! current_user_can( 'manage_options' ) ) return;
    ?>
    <div class="wrap">
        <h1><?php echo esc_html( get_admin_page_title() ); ?></h1>
        <form action="options.php" method="post">
            <?php
            settings_fields( 'myplugin_options' ); // output security fields
            do_settings_sections( 'myplugin' ); // output setting sections
            submit_button(); // submit button            
            ?>
        </form>
    </div>
    <?php
}
```

* ### admin settings
```php
function myplugin_register_settings() {
    register_setting( 
        'myplugin_options', //string   $option_group, 
        'myplugin_options', //string   $option_name, 
        'myplugin_callback_validate_options' //callable $sanitize_callback = ''
    );
    add_settings_section( 
        'myplugin_section_login', //string   $id,
        esc_html__('Customize Login Page', 'myplugin'), //string   $title,
        'myplugin_callback_section_login', //callable $callback,
        'myplugin'//string   $page
    );
    add_settings_field(
        'custom_title', //string   $id, 
        esc_html__('Custom Title', 'myplugin'), //string   $title,
        'myplugin_callback_field_text', //callable $callback,
        'myplugin', //string   $page,
        'myplugin_section_login', //string   $section = 'default',
        [ 'id' => 'custom_title', 'label' => esc_html__('Title attribute', 'myplugin') ] //array $args = []
    );
add_action( 'admin_init', 'myplugin_register_settings' );
```

### Prevent Plugins

* prevent plugins from being deactivated
```php
add_filter( 'plugin_action_links', 'disable_plugin_deactivation', 10, 4 );
function disable_plugin_deactivation( $actions, $plugin_file, $plugin_data, $context ) {
 
    if ( array_key_exists( 'deactivate', $actions ) && in_array( $plugin_file, array(
        'wpforms/wpforms.php',
        'woocommerce/woocommerce.php'
    )))
        unset( $actions['deactivate'] );
    return $actions;
}
```
---

## WPEngine

* [Platform Settings](https://wpengine.com/support/platform-settings/)

* is wpe environment && legacy staging
`is_wpe_snapshot()`

* is wpe environment !& legacy staging
`is_wpe()`

```php
if (function_exists('is_wpe')) {
 echo is_wpe();
} else {
 echo "The function does not exist";
}
```

DISABLE_FILE_MOD
DISABLE_FILE_EDIT

---

## Multisite

```php
define( 'WP_ALLOW_MULTISITE', true );
define( 'MULTISITE', true );
define( 'SUBDOMAIN_INSTALL', false );
$base = '/';
define( 'DOMAIN_CURRENT_SITE', 'wp.local' );
define( 'PATH_CURRENT_SITE', '/' );
define( 'SITE_ID_CURRENT_SITE', 1 );
define( 'BLOG_ID_CURRENT_SITE', 1 );
```

---

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


https://docs.wp-rocket.me/article/131-redirection-to-enforce-trailing-slash-on-urls
# Force trailing slash
RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_METHOD} GET
RewriteCond %{REQUEST_URI} !(.*)/$
RewriteCond %{REQUEST_FILENAME} !\.(gif|jpg|png|jpeg|css|xml|txt|js|php|scss|webp|mp3|avi|wav|mp4|mov)$ [NC]
RewriteRule ^(.*)$ https://%{HTTP_HOST}/$1/ [L,R=301]