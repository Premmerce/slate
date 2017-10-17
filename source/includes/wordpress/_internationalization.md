## Internationalization
Переклади для плагіну повинні мати простір імен(домен). 
Самі файли перекладів не підгружаються автоматично їх потрібно загрузити по action 'init', 
за допомогою функції `load_plugin_textdomain`

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

### Процес перекладу

В корні плагіну створюємо папку languages, через poedit створюємо файли перекладів для кожної мови окремо.
Файли перекладів повинні мати таке саме ім'я як плагін 

[Інструкція по poedit]('http://www.gsy-design.com/how-to-generate-a-pot-file-using-poedit/')


