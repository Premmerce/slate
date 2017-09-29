## Filters Reference

### save_post_{post_type}
Хук що спрацьовує при збереженні поста типу post_type. Для товарів, save_post_product  

Тип: action  
Параметри:  

1. int $post_id   - post id
2. WP_Post  $post - post object
3. bool $updated  - whether this is an existing post being updated or not.

### wp_trash_post
Хук що спрацьовує при пересенні поста в корзину

Тип: action  
Параметри:

1. int $post_id - Post ID