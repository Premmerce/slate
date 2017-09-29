## Internationalization
Переклади для плагіну повинні мати простір імен(домен). 
Самі файли перекладів не підгружаються автоматично їх потрібно загрузити по action 'init'

>Загрузка файлів перекладу

```php
<?php
add_action( 'init', [ $this, 'loadTextDomain' ] );

/**
 * Load plugin translations
 */
public function loadTextDomain() {
    load_plugin_textdomain( 'translation-domain', false,  'plugin_name/languages/' );
}
```


Для виводу перекладеної строки потрібно викликати  __() або _e();

>Повернути перекладену строку

```php
__($message, $domain)
```

>Вивести перекладену строку

```php
виводить дані - _e($message, $domain)
```