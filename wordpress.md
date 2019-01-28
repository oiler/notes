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

```php
//https://developer.wordpress.org/reference/classes/wp_query/parse_query/
$args = array(
  'numberposts' => 10,
  'post_type'   => 'book'
);
$latest_books = get_posts( $args );

```


https://developer.wordpress.org/reference/functions/shortcode_atts/

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

add admin menu item
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

admin display settings callback
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

admin settings
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