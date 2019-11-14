# Woocommerce Product Loop
Aufgabe war das Verhalten des Product Loop anzupassen.
Neu soll beim Klick auf das Produkt in der Übersicht nicht die Einzelansicht geladen werden,
sondern eine Lightbox mit dem Produktbild geöffnet wrden.

Zudem soll der Warenkorb Knopf nur noch erscheinen wenn das Produkt auch auf Lager ist.

Dafür sind folgende Anpassungen nötig:

Im Child-Theme "creattica-premium-child" in der  "functions.php"
folgende Anpassungen machen:

Direkt am Anfang (nach dem <?php Tag) einfügen 
```php
/**  
 * Change Loop Item behavior 
 * do not open single product but show lightbox 
 * of featured image instead 
**/
function plc_switch_loop_productlink(){  
	remove_action( 'woocommerce_template_loop_product_link_open', 10 );  
	add_action( 'woocommerce_before_shop_loop_item', 'plc_before_shop_loop_item', 15 );  
}  
function plc_before_shop_loop_item() {  
  // load product  
  global $product;  
  // get featured image attachment id  
  $post_thumbnail_id = $product->get_image_id();  
  // get image source  
  $sSrc = wp_get_attachment_image_src($post_thumbnail_id,'full');  
  // print link for lightbox  
  echo '<a href=" '.$sSrc[0].'" data-rel="lightbox-gallery-'.$product->get_id().'" class="no-lightbox">';  
}  
add_action( 'woocommerce_before_shop_loop_item', 'plc_switch_loop_productlink' );
```

So haben wir mal die Lightbox eingebaut. Nun noch den Warenkorb Button.

Hierfür folgende Anpassungen im  Child-Theme "creattica-premium-child" unter "woocommerce" in der  "content-product.php" machen.

Den folgenden Zeile suchen
```php
do_action('woocommerce_after_shop_loop_item');
```
Und ersetzen mit: 
```php
// only show cart button if product is in stock  
if($product->is_in_stock()) {  
 do_action('woocommerce_after_shop_loop_item');  
} else {  
  echo '</a><p class="stock out-of-stock">Nicht vorrätig</p>';  
}
```

Das wars dann auch schon :)

### Todos
Aktuell keine.
Hinweis: Man könnte beides wohl auf die selbe Art lösen (per Hook oder per if im template) - so sieht
man jedoch gleich beide Methoden.

### Referenzen
Hier noch die Links zu den verwendeten Ressourcen:
[woocommerce-template-hooks](https://docs.woocommerce.com/wc-apidocs/source-function-woocommerce_template_loop_product_link_close.html#1139-1144)

[stackoverflow-frage-1](https://stackoverflow.com/questions/32837968/how-to-get-featured-image-of-a-product-in-woocommerce)

[stackoverflow-frage-2](https://stackoverflow.com/questions/42334598/can-i-modify-woocommerce-functions-within-the-wc-template-functions-php-file-o)
