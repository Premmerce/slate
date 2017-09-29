## Roles and Capabilities

[Roles and Capabilities](https://codex.wordpress.org/Roles_and_Capabilities)  
В Wordpress існують такі поняття як roles та capabilities

* roles - ролі користувачів (Administrator, Editor, Customer)
* capabilities - права для ролі (активація плагіну, видалення поста)

Отримати список всіх ролей та прав можна через ф-ію ```wp_roles()```

>current_user_can

```php
<?php
if ( current_user_can( $capability ) ) {
    //код
}

// Перевірка для конкретного поста
current_user_can( 'edit_post', $post_id );
```

>author_can

```php
<?php
if ( author_can( $post, $capability ) ) {
    //код
}
```

>add_role

```php
<?php
// Створення ролі та перевірка прав:
add_role( $role_name, $display_name, $capabilities );

add_role( 'photo_uploader', 'Photo Uploader', array( 'organize_gallery' ) );
if ( current_user_can( 'organize_gallery' ) ) {
    // код
}
```

>remove_role

```php
remove_role( 'photo_uploader' );
```


### Functions:  

`current_user_can(string $capability, int $object_id) : boolean`    
Перевірка прав для поточного користувача

`user_can(    int|object $user, string $capability) : boolean`  
Перевірка прав для користувача  

`author_can( object|int $post,string $capability ) : boolean`  
Перевірка прав для автора поста   

`add_role( string $role_name, string $display_name, array $capabilities ) : WP_Role|null`  
Додати роль  

`remove_role( $role_name )`  
Видалити роль  


### WP_Role

>WP_Role

```php
<?php
// get the the role object
$role_object = get_role( $role_name );
 
// add $cap capability to this role object
$role_object->add_cap( $capability_name );
 
// remove $cap capability from this role object
$role_object->remove_cap( $capability_name );
```
Це клас який представляє роль у вигляді об'єкту і дозволяє проводити маніпуляції з правами.


> WP_User

```php
<?php
// get user by user ID
$user = new WP_User( $id );
 
// or get user by username
$user = new WP_User( null, $name );

$user->add_role( $role_name );
$user->remove_role( $role_name );
$user->set_role( $role_name );

```
### WP_User

>Маніпуляція з правами

```php
<?php
// check whether the user has a certain capability or role name
if ( $user->has_cap( $cap_name ) ) {
// do something
}
 
// add a capability to the user and grant access to that capability
$user->add_cap( $cap_name );
 
// remove a capability from the user
$user->remove_cap( $cap_name );
 
// remove all capabilities from the user
$user->remove_all_caps();
```
Клас дозволяє керувати ролями та правами для конкретного користувача