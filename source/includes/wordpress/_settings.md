## Settings API
Settings API дозволяє напів автоматично створювати та обробляти сторінки налаштувань.
API дає можливість створювати сторінки, секції на сторінках та поля в секціях.

### register_settings()

Зареєструвати налаштування і дані 

`register_setting( string $option_group, string $option_name, array $args = array() )`

***Params:***

* `string $option_group` - Назва групи   
* `string $option_name` - Назва налаштування  
* `array $args = []` - Опис налаштування  

### unregister_setting()

Відмінити реєстрацію налаштувань

`unregister_setting( string $option_group, string $option_name, callable $deprecated = '' )`


***Params:***

* `string $option_group` - Назва групи   
* `string $option_name` - Назва налаштування  
* `callable $deprecated` - Застарілий параметр

### add_settings_section()

додати нову секцію налаштувань

`add_settings_section( string $id, string $title, callable $callback, string $page )`

***Params:***

* `string $id` - Ідентифікатор секції
* `string $title` - Заголовок
* `callable $callback` - Колбек для виводу контенту секції (текст між заголовком та полями)
* `string $page` - Сторінка на якій будуть виводитись налаштування. Вбудовані сторінки
'general', 'reading', 'writing', 'discussion', 'media'. Також можна створити свою сторінку налаштувань `add_options_page()`

### add_settings_field()

`add_settings_field( string $id, string $title, callable $callback, string $page, string $section = 'default', array $args = array() )`

***Params:***

* `string $id` - Ідентифікатор поля
* `string $title` - Лейбл поля
* `callable $callback` - Колбек для виводу поля
* `string $page` - Сторінка налаштувань
* `string $section = 'default'` - Секція налаштувань
* `array $args = array()` - Додаткові дані які використовуються для виводу поля
    * `label_for` -  Коли передано, поле буде огорнуто в `<label>` з цим атрибутом `for`.
    * `class` - CSS клас який буде додато `<tr>` елемента при виводі.

### settings_fields()

Вивід **nonce**, **action** та **option_page** полів на сторінці налаштувань, які потрібні для безпеки та правильної обробки форми.

`settings_fields( string $option_group )`

***Params:***

* `string $option_group` - Назва групи налаштувань

### do_settings_sections()
 
 Вивести секції привязані до сторінки
 
`do_settings_sections( string $page )`

***Params:***

* `string $page` - slug сторінки

### do_settings_fields()

Вивести поля для секції налаштувань

`do_settings_fields( string $page, string $section )`

***Params:***

* `string $page` - Slug сторінки
* `string $section` - Slug секції

### add_settings_error()

Зареєструвати помилку для сторінки налаштувань

`add_settings_error( string $setting, string $code, string $message, string $type = 'error' )`

***Params:***

* `string $setting` - Slug налаштування
* `string $code` - Slug ідентифікатор помилки
* `string $message` - Повідомлення
* `string $type = 'error'` - Тип помилки 'error'(червоний) або 'updated'(зелений)

### get_settings_errors()

Отримати мопилки налаштувань

`get_settings_errors( string $setting = '', boolean $sanitize = false )`

***Params:***

* `string $setting = ''` - Slug налаштувань
* `boolean $sanitize = false` - Очистити повідомлення

### settings_errors()

Вивести повідомлення

`settings_errors( string $setting = '', bool $sanitize = false, bool $hide_on_update = false )`

***Params:***

* `string $setting = ''` - Slug налаштування
* `bool $sanitize = false` - Очистити повідомлення
* `bool $hide_on_update = false` - Якщо true помилки будуть виводитись якщо сторінка вже була засабмічена

## Options API
Options API дає можливість, зберігати, читати, оновлювати налаштування плагіну в БД.

### add_option()

Додати нову опцію

`add_option(string $option, mixed $value = '', string $deprecated = '', string|bool $autoload = 'yes')`

***Params:***

* `string $option` - Ключ
* `mixed $value = ''` - Значення
* `string $deprecated = ''` - Не використовується
* `string|bool $autoload = 'yes'` - Загружати автоматично

### add_site_option()

Додати нову опцію для поточного сайту

`add_site_option(string $option, mixed $value)`

***Params:***

* `string $option` - Ключ
* `mixed $value = ''` - Значення

### get_option()

Отримати значення

`get_option( string $option, mixed $default = false )`

***Params:***

* `string $option` - Ключ
* `mixed $default = false` - Значення за замовчуванням

### get_site_option()

Отримати значення для поточного сайту

`get_site_option(string $option, mixed $default = false, bool $deprecated = true)`

***Params:***

* `string $option` - Ключ
* `mixed $default = false` - Значення за замовчуванням
* `bool $deprecated = true` - Не викоритовується

### update_option()

Оновити опцію
 
`update_option( string $option, mixed $value, string|bool $autoload = null )`

***Params:***

* `string $option` - Ключ
* `mixed $value` - Значення
* `string|bool $autoload = null` - Підгружати автоматично 

### update_site_option()
Оновити опцію для поточного сайту

`update_site_option(string $option, mixed $value)`

***Params:***

* `string $option` - Ключ
* `mixed $value` - Значення

### delete_option()
Видалити опцію

`delete_option( string $option )`

***Params:***

* `string $option` - Ключ


### delete_site_option()
Видалити опцію для поточного сайту

`delete_site_option(string $option)`

***Params:***

* `string $option` - Ключ

## Settings page

>Ініціалізація налаштувань

```php
<?php

function premmerce_settings_init() {
	// Зареєструвати налаштування "premmerce" page
	register_setting( 'premmerce', 'premmerce_options' );

	// Зареєструвати секцію на сторінці "premmerce"
	add_settings_section(
		'premmerce_section',
		'Секція',
		'premmerce_section_callback',
		'premmerce'
	);

	// Зареєструвати поле в секції "premmerce_section"
	add_settings_field(
		'premmerce_field_input',

		'Input',
		'premmerce_input_callback',
		'premmerce',
		'premmerce_section',
		[
			'label_for' => 'premmerce_field_input',
		]
	);
}

function premmerce_section_callback() {
	echo "<p>Контент секції</p>";
}

function premmerce_input_callback( $args ) {

	$option = get_option( 'premmerce_options' )
	?>
    <input type="text" name="premmerce_options[<?= esc_attr( $args['label_for'] ); ?>]"
           value="<?= $option[ $args['label_for'] ] ?>">
	<?php
}

/**
 * Реєстрація premmerce_settings_init по хуку admin_init
 */
add_action( 'admin_init', 'premmerce_settings_init' );

```

>Реєстрація та вивід сторінки налаштувань

```php
<?php

function premmerce_options_page() {
	// Додати меню верхнього рівня
	add_menu_page(
		'Premmerce settings',
		'Premmerce settings',
		'manage_options',
		'premmerce-settings',
		'premmerce_options_page_html'
	);
}

/**
 * Зареєструвати premmerce_options_page по хуку admin_menu
 */
add_action( 'admin_menu', 'premmerce_options_page' );


function premmerce_options_page_html() {
	// Перевірка прав доступу
	if ( ! current_user_can( 'manage_options' ) ) {
		return;
	}

	// Перевірити чи користувач засабмітив налаштування
	// Wordpress додає "settings-updated" до $_GET
	if ( isset( $_GET['settings-updated'] ) ) {
		// Додати повідомлення "updated"
		add_settings_error( 'premmerce_messages', 'premmerce_message', 'Settings Saved', 'updated' );
	}

	// Показати повідомлення повідомлення error/update
	settings_errors( 'premmerce_messages' );

	?>
    <div class="wrap">
        <h1><?php echo esc_html( get_admin_page_title() ); ?></h1>
        <form action="options.php" method="post">
			<?php
			// Поля для безпеки для зареєстрованих налаштувань "premmerce"
			settings_fields( 'premmerce' );

			// Вивід секцій налаштувань та їх полів
			do_settings_sections( 'premmerce' );

			// Кнопка збереження
			submit_button( 'Save Settings' );
			?>
        </form>
    </div>
	<?php
}
```
Повний приклад створення сторінки налаштувань. 
Для створення сторінки налаштувань потрібно зареєструвати налаштування `register_setting` 
додати секції  `add_settings_section` та поля `add_settings_field` по хуку `admin_init`, 
додати сотрінку до меню та вивести налаштування за допомогою `settings_fields`, `do_settings_sections`
та `submit_button`, збереження налаштувань будуть оброблятися автоматично.