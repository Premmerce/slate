## Users

> Створення користувача

```php
<?php
// Перевірити чи не зайняте ім'я користувача
$user_id = username_exists($user_name);
 
// Перевірити чи email не належить існуючому користувачу
if (!$user_id && email_exists($user_email) === false) {
// Згенерити пароль
    $random_password = wp_generate_password(
        $length = 12,
        $include_standard_special_chars = false
    );
// створити користувача
    $user_id = wp_create_user(
        $user_name,
        $random_password,
        $user_email
    );
}
```

> Оновлення користувача

```php
<?php
$user_id = 1;

$website = 'https://premmerce.com';
 
$user_id = wp_update_user(
    [
        'ID'       => $user_id,
        'user_url' => $website,
    ]
);
 
if (is_wp_error($user_id)) {
    // error
} else {
    // success
}
```

### wp_create_user()

Створити нового користувача  

`wp_create_user(string $username, string $password, string $email = '')`

***Params:***

* `string $username` - Ім'я
* `string $password` - Пароль
* `string $email = ''` - Email

***Return:***

* `int|WP_Error` - Id створеного користувача або об'єкт WP_Error, 
якщо користувач не може бути створений

### wp_insert_user()

Записати користувача в БД

`wp_insert_user(array|object|WP_User $userdata)`

***Params:***

* `array|object|WP_User $userdata` - Дані користувача
    * `ID` - ID користувача, якщо передано користувача буде оновлено.
    * `user_pass` - пароль.
    * `user_login` - Username для авторизації.
    * `user_nicename` - URL-friendly ім'я користувача.
    * `user_url` - URL.
    * `user_email` - Email.
    * `display_name` - Ім'я для виводу. Default username.
    * `nickname` - Нікнейм. Default username.
    * `first_name` - Ім'я.
    * `last_name` - По батькові.
    * `description` - Біографія користувача.
    * `rich_editing` - Включити rich-editor для користувача.
    * `comment_shortcuts` - Включити keyboard shortcuts для модерації коментів. Default false.
    * `admin_color` - кольорова схема адмінки для користувача. Default 'fresh'.
    * `use_ssl` - Користувач повинем заходити в адмінку через https. Default false.
    * `user_registered` - Дата реєстрації. Формат is 'Y-m-d H:i:s'.
    * `show_admin_bar_front` - Чи відображати адмін панель на фронті
    * `role` - роль користувача.
    * `locale` - локаль користувача.

### wp_update_user()

Оновити користувача

`wp_update_user(array|object|WP_User $userdata)`

***Params:***

* `array|object|WP_User` - дані користувача

### wp_delete_user()

Видалити користувача та мета дані

`wp_delete_user(int $id, int $reassign = null)`

***Params:***

* `int $id` - id користувача
* `int $reassign` - id користувача на якого переасайнити пости ітп.


## User Meta
Користувачі як і пости можуть мати свої мета дані (кастомні поля) 

### add_user_meta()

Додати мета поле для користувача

`add_user_meta(int $user_id, string $meta_key, mixed $meta_value, bool $unique = false)`

***Params:***

* `int $user_id` - id
* `string $meta_key` - ключ
* `mixed $meta_value` - значення
* `bool $unique = false` - Чи такий самий ключ не повинен додаватись

### update_user_meta()

Оновити метадані користувача

`update_user_meta(int $user_id, string $meta_key, mixed $meta_value, mixed $prev_value = '')`

***Params:***

* `int $user_id` - Id
* `string $meta_key` - Ключ   
* `mixed $meta_value` - Значення
* `mixed $prev_value = ''` - Попереднє значення, для перевірки перед видаленням

***Return:***

* `int|bool` - Мета id якщо ключ не існує, true - при оновленні існуючого, false при невдачі

### delete_user_meta()

Видалити мета дані користувача

`delete_user_meta(int $user_id, string $meta_key, mixed $meta_value = '')`

***Params:***

* `int $user_id` - id
* `string $meta_key` - Ключ
* `mixed $meta_value = ''` - Значення

### get_user_meta()

Отримати мета дані користувача

`get_user_meta(int $user_id, string $key = '', bool $single = false)`

***Params***

* `int $user_id` - id користувача
* `string $key = ''` - ключ, за замовчуванням дістаються дані для всіх ключів
* `bool $single = false` - повернути одне значення.