# Woocommerce Category Description for Products

Im Child-Theme "creattica-premium-child" unter "woocommerce" im Template "content-product.php"
folgende Anpassungen machen. Sollte die Datei noch nicht vorhanden sein, wie immer die Vorlage
kopieren aus [WORDPRESS-VERZEICHNIS]/wp-content/plugins/woocommerce/templates/ ins Verzeichnis "woocommerce"
im oben erwähnten Child-Theme.

Direkt unter 
```php
do_action( 'woocommerce_after_shop_loop_item_title' );
```

Den folgenden Code einfügen
```php
/**
    Product Category Description by Nathanael Kammermann
**/
$terms = get_the_terms( $product->ID, 'product_cat' );
echo '<span style="font-size:12px; color:#333;">';
foreach ($terms as $term) {
    echo $term->description;
    break;
}
echo '</span>';

Das wars dann auch schon :)

### Todos

Hier noch die Links zu den verwendeten Ressourcen:
[stackoverflow frage](https://stackoverflow.com/questions/15303031/woocommerce-get-category-for-product-page)
