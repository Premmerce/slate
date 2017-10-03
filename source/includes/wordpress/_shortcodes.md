## Shortcodes

> Створення shortcode

```php
<?php

function premmerce_init_shortcodes() {
	
	add_shortcode( 'h1', function ( $atts, $content , $tag) {
		return "<{$tag} data-attribute='{$atts['data']}'>" . $content . "</{$tag}>";
	} );
	

	add_shortcode('image', function($atts){

		// Комбінація зі значеннямим за замовчуванням
		$atts = shortcode_atts([
			'src' => null
		], $atts);


		return "<img src='{$atts['src']}'>";
	});
}

add_action( 'init', 'premmerce_init_shortcodes' );
```

> Використання всередині поста

```
//double
[h1 data="home"]HOOOOO[/h1]

//single
[image src="https://www.w3schools.com/css/paris.jpg"]
```



Викорестання php коду всередині контенту заборонене, shortcodes дають можливість 
створювати динамічний контент. Shortcodes - це макроси які дають можливість розширювати контент
наприклад, додати до поста галерею або  інший динамічний контент.
Wordpress надає API для створення шоткодів таких як `[gallery id="123" size="medium"]`
для реєстрації shortcode існує функція `add_shortcode`, куди передається тег, 
за яким викликатиметься shortcode та колбек який оброблятиме вивід shortcode. 
Після створення shortcode буде доступний для виклику всередині контенту(наприклад в описі поста)
`[tag]` або `[tag attr1="value1" , attr2="value2"]Some conetent[/tag]`. 

Колбек для виводу шоткодів приймає три параметри:

* array $atts - Масив атрибутів переданих в шоткод
* string $content = null - Контент всередині тегів
* string $tag = null - Тег шоткоду




### Вбудовані shortcodes
За замовчуванням в Wordpress існують такі shortcodes:

* `[caption]`
* `[gallery]`
* `[audio]`
* `[video]` 
* `[playlist]`
* `[embed]`


### add_shortcode()

Створити shortcode

`add_shortcode(string $tag, callable $func)`

***Params:***

* `string $tag` - Тег
* `callable $func` - Колбек

<aside class="notice">
Рекомендується створювати shortcode всередині хука `init`
</aside>

###remove_shortcode()
Видалити shortcode

`remove_shortcode( string $tag )`

***Params:***

* `string $tag` - Тег

###shortcode_exists()
Перевірка чи shortcode існує

`shortcode_exists(string $tag)`

***Params:***

* `string $tag` - Тег

###shortcode_atts()

Комбінує введені атрибути з заданими дефолтними значеннями

`shortcode_atts( array $pairs, array $atts, string $shortcode = '' )`

***Params:***

* `array $pairs` - Масив ключів та дефолтних значень
* `array $atts` - Атрибути ввндені користувачем
* `string $shortcode = ''` - Назва shortcode

###do_shortcode()

Викликати шорткод. Можна використовувати для виклику shortcode всередині php файлу.

`do_shortcode(string $content, bool $ignore_html = false)`

`do_shortcode('[gallery]')`

***Params:***

* `string $content` - Контент шорткоду
* `bool $ignore_html = false` Шорткоди всередині HTML будуть пропущені
