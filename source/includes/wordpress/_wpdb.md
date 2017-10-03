## WPDB

>get_var

```php
<?php
$user_count = $wpdb->get_var( "SELECT COUNT(*) FROM $wpdb->users" );
echo "<p>User count is {$user_count}</p>";
```

>get_row

```php
<?php
global $wpdb;

//об'єкт
$link = $wpdb->get_row( "SELECT * FROM $wpdb->links WHERE link_id = 10" );
echo $link->link_id; //"10"

//асоціативний масив
$link = $wpdb->get_row( "SELECT * FROM $wpdb->links WHERE link_id = 10", ARRAY_A );
echo $link['link_id']; //"10"

//масив
$link = $wpdb->get_row( "SELECT * FROM $wpdb->links WHERE link_id = 10", ARRAY_N );
echo $link[1]; //"10"

//перевірка чи є результат
if ( null !== $link ) {
  // запис знайдений
} else {
  // не знайдено
}
```

>get_results

```php
<?php
global $wpdb;
$fives_drafts = $wpdb->get_results( 
	"
	SELECT ID, post_title 
	FROM $wpdb->posts
	WHERE post_status = 'draft' 
		AND post_author = 5
	"
);

foreach ( $fives_drafts as $fives_draft ) 
{
	echo $fives_drafts->post_title;
}
```

>insert

```php
<?php
global $wpdb;

$wpdb->insert( 
	'table', 
	array( 
		'column1' => 'value1', 
		'column2' => 123 
	), 
	array( 
		'%s', 
		'%d' 
	) 
);

//ід вставленого значення
$id = $wpdb->insert_id;
```

>update

```php
<?php
global $wpdb;

$wpdb->update( 
	'table', 
	array( 
		'column1' => 'value1',	// string
		'column2' => 'value2'	// integer (number) 
	), 
	array( 'ID' => 1 ), 
	array( 
		'%s',	// value1
		'%d'	// value2
	), 
	array( '%d' ) 
);
```

>delete

```php
<?php
global $wpdb;

$wpdb->delete( 'table', array( 'ID' => 1 ) );

// З форматуванням
$wpdb->delete( 'table', array( 'ID' => 1 ), array( '%d' ) );
```

>query

```php
<?php
global $wpdb;

$wpdb->query( 
	//підготовлений запит
	$wpdb->prepare( 
		"
                DELETE FROM $wpdb->postmeta
		 WHERE post_id = %d
		 AND meta_key = %s
		",
	        13, 'gargle' 
        )
);
```

>prepare

```php
<?php
global $wpdb;

$metakey	= "Harriet's Adages";
$metavalue	= "WordPress' database interface is like Sunday Morning: Easy.";

$wpdb->query( $wpdb->prepare( 
	"
		INSERT INTO $wpdb->postmeta
		( post_id, meta_key, meta_value )
		VALUES ( %d, %s, %s )
	", 
        10, 
	$metakey, 
	$metavalue 
) );
```

WPDB - Це об'єкт для абстракції доступу до БД

[Code reference](https://developer.wordpress.org/reference/classes/wpdb/)

$wpdb - доступний як глобальна змінна і його можна використовувати в будь якій частині коду.


<aside class="warning">
    Назву таблиці в запитах необхідно брати з об'єкту $wpdb для вбудованих таблиць (пр. $wpdb->posts), 
    та `$wpdb->prefix . 'table_name'` для кастомних таблиць
</aside>

### get_var()

Отримати одну змінну з БД

`$wpdb->get_var( $query, $column_offset, $row_offset )`

***Params:***

* `string $query` - SQL
* `int $column_offset = 0` - номер колонки
* `int $row_offset = 0` - номер рядка


### get_row()
Отримати рядок

`$wpdb->get_row($query, $output_type, $row_offset)`

***Params:***

* `string $query` - SQL
* `string $output_type` - тип який буде повернено, одна з констант:
    * OBJECT - об'єкт.
    * ARRAY_A - асоціативний масив.
    * ARRAY_N - нумерованиий масив.
* `int $row_offset` - номер колонки


### get_col()

Отримати колонку

`$wpdb->get_col($query, $column_offset)`

***Params:***

* `string $query` - SQL
* `int $column_offset = 0` - номер колонки

### get_results()

Отримати всі дані

`$wpdb->get_results($query, $output_type)`

***Params:***

* `string $query` - SQL
* `string $output_type` - тип який буде повернено, одна з констант:
    * OBJECT - масив об'єктів.
    * OBJECT_K - масив об'єктів з ключами з першої колонки.
    * ARRAY_A - масив асоціативних масивів.
    * ARRAY_N - масив нумерованиич масивів.
    
### insert()

Вставити рядок в БД

`$wpdb->insert($table, $data, $format)`

***Params:***

* `string $table` - таблиця
* `array $data` - дані для вставки (колонка=>значення)
* `array|string $format = null` - формат


### replace()

Замінити рядок якщо такий існує, або створити новий

`$wpdb->replace( $table, $data, $format )`

***Params:***

* `string $table` - таблиця
* `array $data` - дані для вставки (колонка=>значення)
* `array|string $format = null` - формат

### update()

Оновити рядок в таблиці

`$wpdb->update($table, $data, $where, $format = null, $where_format = null )`


***Params:***

* `string $table` - таблиця
* `array $data` - дані для вставки (колонка=>значення)
* `array $where` - дані для умови where (колонка=>значення)
* `array|string $format = null` - формат
* `array $where_format = null` - формат для умови where


### delete()

Видалити рядки

`$wpdb->delete($table, $where, $where_format = null)`

***Params:***

* `string $table` - таблиця
* `array $where` - дані для умови where (колонка=>значення)
* `array $where_format = null` - формат для умови where

### query()

Для виконання кастомних запитів

`$wpdb->query(string $query)`

***Params:***

* `string $query` - SQL

<aside class="warning">
В Цілях безпеки від SQL ін'єкцій, всі запити<br>  
необхідно проганяти через `$wpdb->prepare()`
</aside>

### prepare()

Очищує дані перед запитом, для захисту від SLQ Injection.

`$wpdb->prepare( $query , value_parameter[, value_parameter ... ] )`


***Params:***

* `string $query` - SQL
* `int|string|array value_parameter` - параметри

### Вивід/Відключення виводу sql помилок

Вивід помилок можна влючити/відключити використовуючи наступні функції

* `$wpdb->show_errors()`  
* `$wpdb->hide_errors()`  
* `$wpdb->print_error()`  

### Властивості класу wpdb

* `$show_errors` - Чи виводяться помилки.
* `$num_queries` - Кількість викликаних запитів.
* `$last_query` - Останній виконаний запит.
* `$last_error` - Остання помилка MySQL.
* `$queries` - Можна зберегти всі викликані запити до бази та їхній час встановивши константу SAVEQUERIES = TRUE.
* `$last_result` - Останні результати запиту.
* `$col_info` - Інформація колонки останнього запиту.
* `$insert_id` - ID згенерована AUTO_INCREMENT колонка з останнього inset запиту.
* `$num_rows` - Кількість рядків повернених при останньому запиті.
* `$prefix` - Префікс встановлений вордпресом для таблиць для сайту.
* `$base_prefix` - Оригінальний префікс визначений в wp-config.php.

### Multi-Site Variables
При використанні Multi-Site, також доступні наступні значення:

* `$blogid` - Id поточного сайту(блогу).
* `$siteid` - Id поточної мережі. WordPress зараз підтримує тільки одну мережу на multi-site установку, але це зміниться в майбутньому.

### Tables
Назви таблиць

* `$posts` - Пости.
* `$postmeta` - Мета дані поста.
* `$comments` - Коментарі.
* `$commentmeta` - Мета дані коментарів.
* `$termmeta` - Мета дані термів.
* `$terms` - Терми.
* `$term_taxonomy` - Таксономії.
* `$term_relationships` - Звязки між term та об'єктом який використовує term.
* `$users` - Користувачі.
* `$usermeta` - Мета дані користувачів.
* `$links` - Лінки.
* `$options` - Опції.


### Multisite Tables

Ці таблиці використовуються тільки в multisite установках

* `$blogs` - Список блогів (сайтів) всередині мережі.
* `$signups` - Таблиця реєстрацій.
* `$site` - Скписок мереж.
* `$sitemeta` - Опції всієї установки multisite.
* `$sitecategories` - Категорії сайту.
* `$registration_log` - Лог реєстрація.
* `$blog_versions` - Таблиця версій блогу.

