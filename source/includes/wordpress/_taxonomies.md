## Taxonomies
Таксономія це спосіб групувати елементи.
Наприклад для того щоб погрупувати пости по категоріях використовуються таксономії.
Інші приклади таксономій в Wordpress + Woocommerce:

* теги
* категорії
* атрибути
* бренди

При створеннні нової таксономії вона автоматично додається до меню.
На сторінці таксономії можна керувати термами (значеннями) таксономії (створювати, видаляти, редагувати).
Та до сторінки поста в адмінці додається вибір термів таксономії.

> Реєстрація таксономії

```php
<?php
function post_group_init() {
	// create a new taxonomy
	register_taxonomy(
		'post_group',
		'post',
		[
			'label'        => __( 'Post group' ),
		]
	);
}

add_action( 'init', 'post_group_init' );
```

> Запит постів по таксономії
```php
<?php
$query = new WP_Query( array( 'post_group' => 'archive' ) );
```

### register_taxonomy()

Зареєструвати нову таксономію

`register_taxonomy(string $taxonomy, $object_type, $args)`

***Params:***

* `string $taxonomy` - Назва таксономії
* `$object_type` - Тип поста (вбудований або кастомний)
* `$args` - Аргументи (див. [register taxonomy](https://codex.wordpress.org/Function_Reference/register_taxonomy))

### wp_set_object_terms()

Встановити терми для об'єкта, замінить всі терми заданої таксономії для об'єкта з переданим id.

`wp_set_object_terms($object_id, $terms, $taxonomy, $append)`

***Params:***

* `int $object_id` - id поста
* `array|int|string $terms` - slud, id терма або масив (slug або id)
* `array| string $taxonomy` - назва таксономії
* `boolean $append = false`- замінити терми якщо false, чи додати нові якщо true

### get_terms()

Отримати терми

`get_terms(string|array $args = array(), array $deprecated = '')`

***Params:***

* `string|array $args = array()` - Аргументи для запиту(див. [WP_Term_Query::__construct()](https://developer.wordpress.org/reference/classes/wp_term_query/__construct/) )
* `array $deprecated = ''` - Для підтримки старого коду