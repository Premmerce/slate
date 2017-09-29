## Hooks
Хуки створені для того щоб надати можливість розширювати функціонал вордпрес не змінюючи коду
ядра. Існують два типи хуків Filter та Action.

## Actions

Actions - це функції які виконуються при певній події, 
наприклад при збереженні поста, зміні теми, відображені сторінки.

### Перевірка чи існує подія
`has_action( string $tag, callable $callback)`

### Добавити функцію до події
`add_action( string $tag, callable $callback, int $priority, int $accepted_args)`

### Створити подію 
`do_action( string $tag, mixed $arg)`

### Створити подію з масивом аргументів
`do_action_ref_array(string $tag, array $args)`

### Отримати скільки разів викликалась подія
`did_action(string $tag)`

### Видалити функція підписану на подію
`remove_action(string $tag, callable $callback, int $priority)`

### Видалити всі хуки прикріплені до події
`remove_all_actions(string $tag, int $priority)`

### Перевірити чи зараз виконується подія
`doing_action(string $action)`

## Filters

Filters - Це функції які обробляють дані перед тим як продовжити 
якусь операцію (вивід, запис в БД). Фільтри повинні повертати дані.

### Перевірка чи існує фільтр
`has_filter(string $tag, callable $callback)`


### Додати фільтр
`add_filter(string $tag, callable $callback, int $priority, int $accepted_args)`


### Додати фільтр з масивом аргументів
`apply_filters_ref_array(string $tag, array $args)`

### Отримати назву поточного хука
`current_filter()`

### Видалити фільтр
`remove_filter(string $tag, callable $callback, int $priority)`


### Створення кастомної події для фільтрування
`apply_filters(string $tag, mixed $value)`


###Реєстрація фільтру
`add_filter(string $tag , callable $callback, int $priority, int $accepted_args)`


###Видалити всі хуки для фільтру
`remove_all_filters(string $tag, int $priority)`

### Перевірити чи зараз виконується фільтр
`doing_filter(string $filter)`

