# Woocommerce Breadcrumbs

Im Child-Theme "creattica-premium-child" unter "woocommerce" im Template "archive-product.php"
folgende Anpassungen machen:

Direkt unter 
```php
<?php get_header( 'shop' ); ?>
```

Den folgenden Code einfügen
```php
<!-- Trennlinie oberhalb der Breadcrumbs -->
<hr style="margin-top:-16px; padding-bottom:20px;" />
<?php
/**
  * Woocommerce Breadcrumbs - added by Nathanael Kammermann
 */
$args = array(
  'delimiter' => ' - ',
);
woocommerce_breadcrumb( $args );
```
Dazu in der style.css des selben Child-Themes noch folgenden Eintrag hinzufügen
```css
.woocommerce-breadcrumb {
    padding-left:34px !important;
    margin-top:-20px !important;
    font-size:14px !important;
}
```

Das wars dann auch schon :)

### Todos

Hier noch die Links zu den verwendeten Ressourcen:
[woocommerce-breadcrumbs doc]: <https://docs.woocommerce.com/document/woocommerce_breadcrumb>
