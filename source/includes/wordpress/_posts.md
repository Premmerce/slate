## Posts
Пости це основний тип даних Wordpress, за допомогою постів реалізовані, сторінки, товари, замовлення, пункти меню, зображення.

## Custom post types

>Реєстрація кастомного типу поста

```php
<?php
function custom_post_type() {
	register_post_type( 'premmerce_video',
		[
			'labels'      => [
				'name'          => __( 'Video' ),
				'singular_name' => __( 'Videos' ),
			],
			'public'      => true,
			'has_archive' => true,
		]
	);
}

add_action( 'init', 'custom_post_type' );
```

>Запит кастомного типу

```php
<?php
$args = [
    'post_type'      => 'premmerce_video',
    'posts_per_page' => 10,
];
$loop = new WP_Query($args);
while ($loop->have_posts()) {
    $loop->the_post();
    ?>
    <div class="entry-content">
        <?php the_title(); ?>
        <?php the_content(); ?>
    </div>
    <?php
}
?>
```

>Розширення main query для вибірки кастомного типу

```php
<?php
function wporg_add_custom_post_types($query)
{
    if (is_home() && $query->is_main_query()) {
        $query->set('post_type', ['post', 'page', 'premmerce_video']);
    }
    return $query;
}
add_action('pre_get_posts', 'wporg_add_custom_post_types');

```
За замовчуванням в Wordpress 5 типів постів:

* post
* page
* attachment
* revision
* nav_menu_item
* custom_css
* customize_changeset

При розробці плагіну часто потрібно реалізувати свої типи постів наприклад, товари для e-commerce сайтів
відео для сайтів з оглядами. Для того щоб додати свій потрібно зареєструвати новий post_type за допомогою `register_post_type`.
Новий тип за замовчуванням не буде автоматично вибиратися з бази на сторінці постів, але цю поведінку можна змінити шляхом
розширення головного запиту (main query) (див. приклад праворуч). 

### register_post_type()
Реєстрація типа поста

`register_post_type( string $post_type, array|string $args = array() )`

***Params:***   
`string $post_type` - Унікальний ключ типу  
`array $args` - Масив з описом типу([register post type](https://developer.wordpress.org/reference/functions/register_post_type/))  


<aside class="warning">
Функція register_post_type() повинна викликатись перед `admin_init` та після `after_setup_theme` хуків.
Найкращий варіант використовувати хук `init`.
</aside>
<aside class="warning">
Для того щоб уникнути конфліктів між плагінами ідентифікатор повинен бути унікальним
</aside>