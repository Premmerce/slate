## Create plugin

>Заголовки в файлі плагіну.

```php
/**
 * Plugin Name: Name
 * Plugin URI: http://сторінка-плагіну
 * Description: Short description
 * Version: Версія, наприклад: 1.0
 * Author: Автор
 * Author URI: http://сторінка-автора
 * License:      GPL2
 * License URI:  https://www.gnu.org/licenses/gpl-2.0.html
 * Text Domain:  domain-name
 * Domain Path:  /languages
 */
```

[Повна документація](https://developer.wordpress.org/plugins/)  
Для створення плагіну достатньо створити php файл в папці 
/wp-content/plugins. Файл повинен містити інформаційний заголовок, 
якщо плагін потребує більше файлів створюємо папку в яку кладемо головний файл плагіну.
[Повна документація по заголовкам](https://developer.wordpress.org/plugins/the-basics/header-requirements/)

## Activation/Deactivation/Uninstall

>Зареєструвати хук активації

```php
<?php
register_activation_hook( __FILE__, 'callback' );
```

>Зареєструвати хук деактивації

```php
<?php
register_deactivation_hook( __FILE__, 'callback' );
```

>Зареєструвати хук видалення

```php
<?php
register_uninstall_hook(__FILE__, 'callback');
```

Для того щоб виконати певні операції при встановленні/деактивації/видаленні плагіну використовуються хуки.
Таким чином можна зареєструвати колбек, який буде викликатись при цих операціях.
Це портібно для підготвоки оточення для плагіну(створення таблиць в БД, початкова конфігурація), 
та очистки при деактивації чи видаленні плагіну.

* ```register_activation_hook``` викликається при встановленні плагіну  
* ```register_deactivation_hook``` викликається при деактивації плагіну  
* ```register_uninstall_hook``` викликається при видаленні плагіну  

<aside class="warning">
Через <code>register_uninstall_hook</code> можна зареєструвати тільки функцію або статичний метод класу
</aside>

Різниця між uninstall та deactivation та сценарії:

Scenario|Deactivation|Uninstall
------- | ---------- | --------
Видалити кеш тимчасові файли|так|ні
Видалити пермалінки|так|ні
Видалити налаштування|ні|так
Видалити таблиці з БД|ні|так