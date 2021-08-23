# Render Widget Content

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Intermediate" />

Elementor has a hook that allows developers to change the widget content in the frontend. It will be applied on the final HTML content of a single widget. In the Editor Preview it will be shown after the user finishes editing the element.

## Hook Details

* **Hook Type:** Action Hook
* **Hook Name:** `elementor/widget/render_content`
* **Affects On:** Frontend

## Hook Arguments

| Argument  | Type                       | Description             |
|-----------|----------------------------|-------------------------|
| `content` | _`string`_                 | The widget HTML output. |
| `widget`  | _`\Elementor\Widget_Base`_ | The widget instance.    |

## Change Widget Content

Go over all the `heading` widgets and if the heading use external links, add an icon after the links indicating it's an external links:

```php
/**
 * Filters heading widgets and change their content.
 *
 * @since 1.0.0
 * @param string                 $widget_content The widget HTML output.
 * @param \Elementor\Widget_Base $widget         The widget instance.
 */
function change_heading_widget_content( $widget_content, $widget ) {

	if ( 'heading' === $widget->get_name() ) {
		$settings = $widget->get_settings();

		if ( ! empty( $settings['link']['is_external'] ) ) {
			$widget_content .= '<i class="fa fa-external-link" aria-hidden="true"></i>';
		}
	}

	return $widget_content;

}
add_action( 'elementor/widget/render_content', 'change_heading_widget_content', 10, 2 );
```

## Notes

To change the [widget JavaScript template](./print-widget-template) see `elementor/widget/print_template`.