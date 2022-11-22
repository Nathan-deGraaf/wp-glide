# WP Glide
A wrapper for PHP Glide/composer. Built for >= php@7.2 and >=php@8.0.

*A build off of the no longer maintained [Aginevs wp-glide wrapper](https://github.com/aginev/).*

## **This is a WIP build**

## **Install**

```src
composer require nathan-degraaf/wp-glide
```

## **Usage**

General configuration could be made at your function.php file in your theme, Though I recommend creating a dedicated glide file for your presets.

### **Create Instance**

It's a singleton instance, so you will get just the same object everywhere in your application.

```php
$wpGlide = wp_glide();
```

### **Server config**

You should config WpGlide at least once in your application. The init method could have four parameters and all of them are not required.

```php
$wpGlide = wp_glide()->init([
    // Glide server config. See: http://glide.thephpleague.com/2.0/config/setup/
  [
    // Image driver
    'driver'     => 'imagick',
    // Watermarks path
    'watermarks' => new \League\Flysystem\Filesystem(new \League\Flysystem\Adapter\Local(get_template_directory() . '/assets/img')),
  ],
  
  // Base path. By default set to 'img/' and the final URL will look like so: http://example.com/BASE-PATH/SIZE-SLUG/image.jpg.
  'img/',
  
  // Path to WordPress upload directory. If not set the default upload directory will be used.
  'upload_path',
  
  // Cache path. If not set the cache will be placed in cache directory at the root of the default upload path.
  'cache_path'
]);
```

### **Register image sizes**

You should register image sizes that will be handled by Glide like so:

```php
$wpGlide->addSize('size_name', [
    'w'  => 1400,
    'q'  => 80,
    'fm' => 'webp',

    'mark'      => 'watermark.png',
    'markw'     => 1000,
    'markh'     => 1000,
    'markalpha' => 55,
    'markfit'   => 'fill',
    'markpos'   => 'center',

])->addSize('size_name_512', [
    'w'  => 512,
    'q'  => 80,
    'fm' => 'webp',

])->addSize('16x9', [
    'w'   => 16 * 10 * 2,
    'h'   => 9 * 10 * 2,
    'fit' => 'crop',
    'q'   => 80,
    'fm'  => 'webp',
]);
```

### **Usage in templates**

```html
<!-- Get Glide image URL by it's original URL -->
<img src="<?php echo wp_glide_image('https://yourimage.com', 'size_name'); ?>" />
```

retrive base64 encoded version: 

```html
<!-- Get Glide image URL by it's original URL -->
<img src="<?php echo wp_glide_base64('http://example.com/image.jpg', 'w128'); ?>" />
```

## **License**
Everything in this repository is MIT License unless specified.

MIT © 2022 Nathan deGraaf
