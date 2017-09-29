# Woocommerce

## Hooks
[WooCommerce hooks reference](https://docs.woocommerce.com/wc-apidocs/hook-docs.html)   
[Wordpress filter reference](https://codex.wordpress.org/Plugin_API/Filter_Reference)  
[Wordpress action reference](https://codex.wordpress.org/Plugin_API/Action_Reference)  
[Wordpress hooks reference](https://developer.wordpress.org/reference/hooks/)  

### woocommerce_get_breadcrumb
Дозволяє підмінити breadcrums  

Тип: filter   

Параметри:  

1. array - breadcrums
2. WC_Breadcrumb - object

### woocommerce_shipping_instance_form_fields_{shipping_title}
Фільтр що повертає масив полів шіппінг методу з назвою shipping_title

Тип: filter

### woocommerce_product_options_general_product_data
Спрацьовує коли формується вкладка General в картці продукту

Тип: action

### woocommerce_process_product_meta
Спрацьовує на збереження продукту

Тип: action

### woocommerce_product_after_variable_attributes
Спрацьовує коли формується форма для кожного варіанту товара

Тип: action

### woocommerce_save_product_variation
Спрацьовує на збереження варіантів товару

Тип: action

### woocommerce_product_get_price
Спрацьовує в той момент коли береться ціна продукту

Тип: filter

### woocommerce_product_get_sale_price
Спрацьовує в той момент коли береться ціна продажу продукту

Тип: filter

### woocommerce_product_variation_get_price
Спрацьовує в той момент коли береться ціна вараінта продукту

Тип: filter

### woocommerce_product_variation_get_sale_price
Спрацьовує в той момент коли береться ціна продажу вараінта продукту

Тип: filter

### woocommerce_variation_prices_price
Спрацьовує коли формується ціна для варіанту (front price range)

Тип: filter

### woocommerce_variation_prices_sale_price
Спрацьовує коли формується ціна для варіанту (front price range)

Тип: filter