## Widgets

> Клас віджету

```php
<?php 

class My_Widget extends WP_Widget {

	public function __construct() {

		parent::__construct(
			'premmerce_widget',  // Base ID
			'Some widget'   // Name
		);

	}


	// Вивід віджету на фронт
	public function widget( $args, $instance ) {

		echo $args['before_widget'];

		if ( ! empty( $instance['title'] ) ) {
			echo $args['before_title'] . apply_filters( 'widget_title', $instance['title'] ) . $args['after_title'];
		}

		echo '<div class="textwidget">';

		echo esc_html__( $instance['text'], 'text_domain' );

		echo '</div>';

		echo $args['after_widget'];

	}

	// Форма налаштувань віджета
	public function form( $instance ) {

		$title = ! empty( $instance['title'] ) ? $instance['title'] : esc_html__( '', 'text_domain' );
		$text = ! empty( $instance['text'] ) ? $instance['text'] : esc_html__( '', 'text_domain' );
		?>
		<p>
			<label for="<?php echo esc_attr( $this->get_field_id( 'title' ) ); ?>"><?php esc_attr_e( 'Title:', 'text_domain' ); ?></label>
			<input class="widefat" id="<?php echo esc_attr( $this->get_field_id( 'title' ) ); ?>" name="<?php echo esc_attr( $this->get_field_name( 'title' ) ); ?>" type="text" value="<?php echo esc_attr( $title ); ?>">
		</p>
		<p>
			<textarea class="widefat" id="<?php echo esc_attr( $this->get_field_id( 'text' ) ); ?>" name="<?php echo esc_attr( $this->get_field_name( 'text' ) ); ?>" type="text" cols="30" rows="10"><?php echo esc_attr( $text ); ?></textarea>
		</p>
		<?php

	}

	// Обробка форми віджета
	public function update( $new_instance, $old_instance ) {

		$instance = array();

		$instance['title'] = ( !empty( $new_instance['title'] ) ) ? strip_tags( $new_instance['title'] ) : '';
		$instance['text'] = ( !empty( $new_instance['text'] ) ) ? $new_instance['text'] : '';

		return $instance;
	}

}

add_action( 'widgets_init', function() {
	register_widget( new My_Widget() );
});

```
Віджети дозволяють додавати контент та різні фічі в сайдбар 
()місця для віджетів визначені в шблоні). Це дає можливість користувачу швидко 
кастомізувати свій сайт.

Віджети це об'єкти php які виводять певний HTML код. При створенні та реєстрації нового віджету 
від зявиться в адмін панелі і буде доступний для виводу на фронт.

Для того щоб створити віджет потрібно створити клас який наслідується від WP_Widget

В класі віджету потрібно реалізувати наступні методи:

* `__construct` - ініціалізація, встановлення description, name
* `widget` - вивід віджету та фронті
* `form` - форма налаштувань віджету
* `update` - збереження налаштувань віджету

<aside class="notice">
Віджети потрібно додавати по хуку `widgets_init`
</aside>

[Wordpress widgets doc](https://developer.wordpress.org/themes/functionality/widgets/)
