# Woocommerce Category Description for Products

Im Child-Theme "creattica-premium-child" unter "woocommerce" im Template "archive-product.php"
folgende Anpassungen machen. Sollte die Datei noch nicht vorhanden sein, wie immer die Vorlage
kopieren aus [WORDPRESS-VERZEICHNIS]/wp-content/plugins/woocommerce/templates/ ins Verzeichnis "woocommerce"
im oben erwähnten Child-Theme.

Direkt über 
```php
<?php get_footer( 'shop' ); ?>
```

Den folgenden Code einfügen
```php
<hr/>
<span style="font-size:14px; margin-left:34px;">
    <?php
    $terms = get_the_terms( $product->ID, 'product_cat' );
    echo '<div style="font-size:14px; color:#333; padding-left: 34px; padding-right:34px;">';
    foreach ($terms as $term) {
        echo '<h3>'.$term->name.'</h3>';
        echo $term->description;
        break;
    }
    echo '</div>';
    ?>
</span>
```

Das wars dann auch schon :)

### Todos

Hier noch die Links zu den verwendeten Ressourcen:
[stackoverflow frage](https://stackoverflow.com/questions/15303031/woocommerce-get-category-for-product-page)
