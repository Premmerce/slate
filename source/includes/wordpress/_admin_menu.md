## Administration menu

>Usage

```php
<?php
add_action( 'admin_menu', function () {
	add_menu_page( 'Plugin page title',
		'Plugin menu title',
		'manage_options',
		'plugin-slug',
		function () {
			echo '<h1>My plugin page</h1>';
		},
		'dashicons-dashboard' );
} );
```

Функції для управління адміністративним меню.

### add_menu_page

Додати сторінку до верхнього рівня меню

`add_menu_page($page_title,  
     $menu_title,  
     $capability,  
     $menu_slug,   
     $function,  
     $icon_url,  
     $position  
)`
  
*Параметри:*  
`string $page_title` - title сторінки  
`string $menu_title` - назва меню  
`string $capability` - права доступу до сторінки  
`string $menu_slug` - slug сторінки
`callable $function` - функція яка відображає контент сторінку  
`string $icon_url` - dashicon або посилання на зображення, за замовчуванням іконки немає
`int $position` -  позиція елементу меню


###add_submenu_page
Додати підменю

`add_submenu_page($parent_slug, $page_title, $menu_title, $capability, $menu_slug, $function)`

*Параметри:*   
`string $parent_slug` - slug пункту меню до якого добавити  
`string $page_title` - title сторінки    
`string $menu_title` - назва меню  
`string $capability` - права доступу до сторінки  
`string $menu_slug` - slug сторінки
`callable $function` - функція яка відображає контент сторінку  

###remove_menu_page
Видалити пункт меню  рівня.

`remove_menu_page(string $menu_slug)`

*Параметри:*  
`string $menu_slug` - slug сторінки 
