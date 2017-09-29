## Validation and Security

### PHP functions

* `isset()` та `empty()` перевірка чи змінна існує і не порожня
* `mb_strlen()` або `strlen()` для перевірки довжини строки
* `preg_match()`, `strpos()` для перевірки чи підстрока в строці
* `count()` перевірка кількості елементів в масиві
* `in_array()` перевірка чи елемент в масиві

### WordPress functions

* `is_email()` перевірка чи email валідний
* `term_exists()` - перевірка чи існує тег категорія чи інший терм
* `username_exists()` - перевірка чи існує користувач з заданим іменем
* `validate_file()` перевірка чи це реальний шлях(існування файлу не перевіряється)

### Securing input
Процес очистки вхідних даних, потрібен коли невідомо які дані можуть прийти, 
або ви не хочете обмежувати користувача валідацією. Для цього в вордпресі існує ряд функцій.



`sanitize_email(string $email)` - очистка недопустимих символів в email.


`sanitize_file_name(string  $name)` - Очистка недопустимих символів в імені файлу.


`sanitize_html_class(string $class, string $fallback)` - Очистка недопустимих символів в html класі


`sanitize_key($key)` - Приведення до нижнього регістру та очистка недопустимих символів в ключі масиву


`sanitize_mime_type(string $mime_type)` - Очистка недопустимих символів mime тип


`sanitize_text_field(string $str)` - 
Очистка строки введеної користувачем або з БД


`sanitize_title( $title, $fallback_title, $context )` - 
Очистка недопустимих символів в назві


`sanitize_title_for_query(string $title)` - 
очистка недопустимих символів для запиту в БД  


`sanitize_title_with_dashes(string $title, string $unused, string('display'|'save') $context)` - 
заміна пробілів на символ `-` 
 

`sanitize_user(string $username, boolean $strict)` - 
очистка недопустимих символів в імені користувача  


`esc url(string $url, array $protocols,string  $_context)` - 
очистка недопустимих символів  


`esc_url_raw(string $url, array $protocols)` - 
очистка недопустимих символів в URL, на відміну від escape_url, не замінює символи для виводу, 
вихідний URL безпечний для БД, редіректів та HTTP запитів  


`wp_filter_post_kses($data)` - 
очистка недопустимих HTML тегів для контенту поста  


`wp_filter_nohtml_kses($data)` - 
очистка всіх HTML тегів 

### Securing output
Очистка виводу. Для цього в вордпресі існує ряд функцій.

* `esc_html()` - Для виводу даних в шаблоні
* `esc_url()` - Для виводу всіх URL
* `esc_js()`- Для inline Javascript.
* `esc_attr()` - Для HTML атрибутів

### Nonces
Nonce(number used once) - це токени, які використовуються для перевірки запитів в цілях безпеки.
Наприклад згенероване посилання для видалення поста
`http://wpmag.ru/wp-admin/post.php?post=123&action=trash&_wpnonce=b192fc4204`

не буде працювати для іншого поста
`http://wpmag.ru/wp-admin/post.php?post=456&action=trash&_wpnonce=b192fc4204`

Також це захист від підробки запитів(CSRF).

Кожен Nonce може використовуватися тільки один раз, і має обмежений термін дії.

`wp_nonce_field( $action, $name, $referer, $echo )` - використовується для генерації nonce


`wp_create_nonce($action)` - генерує nonce


`wp_nonce_url()` - Retrieve URL with nonce added to URL query.


