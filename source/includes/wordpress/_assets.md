## Assets
```php
<?php
// Зареєструвати скрипт
wp_register_script( 'my_plugin_script', 'path/to/myscript.js' );
 
// Локалізувати скрипт
$translation_array = array(
    'some_string' => __( 'Some string to translate', 'my-plugin-domain' ),
    'value' => '10'
);

wp_localize_script( 'my_plugin_script', 'object_name', $translation_array );
 
// Додати скрипт з локалізованими даними.
wp_enqueue_script( 'my_plugin_script' );
?>
<script>
	console.log( object_name.value ); // 10
</script>
```


Вордрес надає функці для коректної загрузки CSS та JS. Основні з них 
`wp_register_script`, `wp_enqueue_script`, `wp_register_style` та `wp_enqueue_style`.
Також в ядрі вордпресу є вже зареєстровані скрипти такі як jquery і.т.п.
[Список скриптів](https://developer.wordpress.org/reference/functions/wp_register_script/#core-registered-scripts)

### wp_register_script
Зареєструвати новий скрипт, для того щоб потім додатии його в чергу на вивід

`
wp_register_script( 
    string $handle, 
    string $src, 
    array $deps = array(), 
    string|bool|null $ver = false, 
    bool $in_footer = false )
`

***Params:***

* `string $handle` - Унікальна назва скрипта  
* `string $src` - Повний URL  
* `array $deps = array()` - Залежності  
* `string|bool|null $ver = false` - Версія
* `bool $in_footer = false` - Підключати скрипт в футері

### wp_enqueue_script
Зареєструвати скрипт та додати в чергу на вивід

`wp_enqueue_script( 
    string $handle, 
    string $src = '', 
    array $deps = array(), 
    string|bool|null $ver = false, 
    bool $in_footer = false 
)`


***Params:***

* `string $handle` - Унікальна назва скрипта  
* `string $src` - Повний URL  
* `array $deps = array()` - Залежності  
* `string|bool|null $ver = false` - Версія
* `bool $in_footer = false` - Підключати скрипт в футері


### wp_register_style
Зареєструвати CSS

`wp_register_style( 
    string $handle, 
    string $src, 
    array $deps = array(), 
    string|bool|null $ver = false, 
    string $media = 'all' 
)`

***Params:***

* `string $handle` - Унікальна назва стилю  
* `string $src` - Повний URL  
* `array $deps = array()` - Залежності  
* `string|bool|null $ver = false` - Версія
* `string $media = 'all'` - Тип медіа('all', 'print', 'screen') або медіа запити (orientation: portrait)' та '(max-width: 640px)


### wp_enqueue_style
Зареєструвати CSS та додати в чергу 

`wp_enqueue_style( 
    string $handle, 
    string $src = '', 
    array $deps = array(), 
    string|bool|null $ver = false, 
    string $media = 'all' 
)`

***Params:***

* `string $handle` - Унікальна назва стилю  
* `string $src` - Повний URL  
* `array $deps = array()` - Залежності  
* `string|bool|null $ver = false` - Версія
* `string $media = 'all'` - Тип медіа('all', 'print', 'screen') або медіа запити (orientation: portrait)' та '(max-width: 640px)

### wp_localize_script
Локалізація скрипта, також може бути використано для передачі значення з php коду в js

`wp_localize_script( 
    string $handle, 
    string $object_name, 
    array $l10n 
);
`

***Params:***

* `string $handle` - Назва скрипта
* `string $object_name` - Назва js обєкту
* `array $l10n` - Масив даних які будуть передані в js об'єкт
