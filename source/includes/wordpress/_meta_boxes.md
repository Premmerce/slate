## Meta Boxes
Мета бокси це окремі контейнери з яких складається сторінка (скрін).
Плагіни можуть розширювати сторінку редагування додаючи свої мета бокси. 
Мета бокси дуже гнучкі, користувач може обирати які з них відображати на сторінці та
змінювати їхні позиції.  
[Wordpress meta boxes docs](https://developer.wordpress.org/plugins/metadata/custom-meta-boxes/)  
### Створення мета бокса
>Додати мета бокс

```php
<?php
function adding_custom_meta_boxes( $post_type, $post ) {
    add_meta_box( 
        'my-meta-box',
        __( 'My Meta Box' ),
        'render_custom_box_html',
        'post',
        'normal',
        'default'
    );
}
add_action( 'add_meta_boxes', 'adding_custom_meta_boxes', 10, 2 );
```

>Додати мета бокс поста типу post

```php
<?php
function adding_custom_meta_boxes( $post ) {
    add_meta_box( 
        'my-meta-box',
        __( 'My Meta Box' ),
        'render_custom_box_html',
        'post',
        'normal',
        'default'
    );
}
add_action( 'add_meta_boxes_post', 'adding_custom_meta_boxes' );
```

>render_custom_box_html

```php
<?php
function render_custom_box_html($post)
{
    ?>
    <label for="wporg_field">Description for this field</label>
    <select name="wporg_field" id="wporg_field" class="postbox">
        <option value="">Select something...</option>
        <option value="something">Something</option>
        <option value="else">Else</option>
    </select>
    <?php
}
```

Для створення метабокса потрібно додати action на `add_meta_boxes`.
Також для конкретного типу поста можна використовувати `add_meta_boxes_{post_type}`

<aside class="notice">
Мета бокси не повинні мати кнопки submit, 
поля мета боксів сабмітяться разом з формою
</aside>


### Збереження даних

>save data

```php
<?php
function wporg_save_postdata($post_id)
{
    if (array_key_exists('wporg_field', $_POST)) {
        update_post_meta(
            $post_id,
            '_wporg_meta_key',
            $_POST['wporg_field']
        );
    }
}
add_action('save_post', 'wporg_save_postdata');
```
Для збереження даних метабоксу потрібно зареєструвати action на `save_post`. 
Якщо потрібно записати дані в post_meta, можна використати функцію `update_post_meta`

### add_meta_box()

Функція додає мета бокс до скріна  
`add_meta_box( string $id, string $title, callable $callback, string|array|WP_Screen $screen = null, string $context = 'advanced', string $priority = 'default', array $callback_args = null )`

***Params:***    
`string $id` - id мета бокса (використовується як html атрибут 'id' )    
`string $title` - Title of the meta box  
`callable $callback` - Колбек для виводу контенту  
`string|array|WP_Screen $screen = null` - Скріни на яких показувати контент (такі як post_type, 'link', or 'comment'). ID, WP_Screen або масив з id скрінів
`string $context = 'advanced'` - Де відображати 'normal', 'side', та 'advanced'  
`string $priority = 'default'` - Пріоритет розташування ('default', 'high', 'low').  
`array $callback_args = null` - Дані які передаються в колбек.  

### remove_meta_box()

Видалити мета бокс

`remove_meta_box( string $id, string|array|WP_Screen $screen, string $context )`

***Params:***   
`string $id` - id мета бокса (використовується як html атрибут 'id' )  
`string|array|WP_Screen $screen = null` - Скріни на яких показувати контент (такі як post_type, 'link', or 'comment'). ID, WP_Screen або масив з id скрінів.  
`string $context = 'advanced'` - Де відображати 'normal', 'side', та 'advanced'.  


