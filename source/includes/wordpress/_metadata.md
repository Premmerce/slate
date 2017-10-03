## Post Meta
Метадата додає можливість додати кастомні дані для поста. 

### Функції для роботи з метаданими.

### add_post_meta()
Додати поле до поста

`add_post_meta($post_id, $meta_key, $meta_value, $unique)`
  
***Params:***  
`int $post_id` - id поста  
`string $meta_key` - ключ  
`string|array $meta_value` - значення, масив буде серіалізований автоматично
`boolean $unique` - унікальність поля  

***Return:***  
int|boolean - id створеного поля або false.  

<aside class="notice">
Для створення прихованого поля meta_key повинен починатися з `_` наприклад `_hidden_meta_key`
</aside>
### update_post_meta
Оновити дані поля для поста

`update_post_meta( $post_id, $meta_key, $meta_value, $prev_value )`


***Params:***  
`int $post_id` - id поста  
`string $meta_key` - ключ  
`mixed $meta_value` - значення  
`mixed $prev_value` - попереднє значення, параматр корисний коли існують декілька
значень з однинаковим ключем.

***Return:***  
int|boolean - id створеного поля якщо такого поля не існує, або true/false.  


### delete_post_meta()
Видалити поле

`delete_post_meta($post_id, $meta_key, $meta_value)`

***Params:***  
`int $post_id` - id поста  
`string $meta_key` - ключ  
`mixed $meta_value` - значення  

***Return:***  
boolean  

### get_post_custom()
Отримати кастомні дані поста

`get_post_custom($post_id)`

***Params:***  
`int $post_id` - id поста  

***Return:***  
array - масив всіх полів поста

### get_post_custom_values()
Отримати масив значень поста для одного поля

`get_post_custom_values($key, $post_id)`

***Params:***  
`string $key` - ключ поля  
`int $post_id` - id поста  

***Return:***  
array - масив значень для поля


### get_post_custom_keys()
Оримати ключі кастомних полів для поста

`get_post_custom_keys($post_id)`  

***Params:***  
`int $post_id` - id поста  

***Return:***  
array - масив ключів

