# Changing the table definition directory

The plugin will attempt to automatically generate a directory to house all related files when an ACF Field Group is saved and the table generation on that field group is active. The possible locations for this directory are:

1. If using ACF JSON, the `acf-json/database-tables` directory will be created.
2. If no acf-json directory is available, the plugin will attempt to create `uploads/acf-custom-database-tables` directory.

It is possible, however, for you to customise the location and name of this directory using either of the following options:

## Using a PHP constant

You can define the following PHP constant in your `wp-config.php` file or in a configuration plugin, provided it is defined before the `plugins_loaded` action hook:

```php
<?php
/*
 * Changes the ACF Custom Database Tables JSON directory.
 * This needs to run before the 'plugins_loaded' action hook, so 
 * you need to put this in a plugin or in your wp-config.php file.
 */
define( 'ACFCDT_JSON_DIR', '/full/path/to/my-custom-json-dir' );
```

Using this approach is definitive and the directory path specified will not be passed to the filter for override. You may need to create this directory yourself and make sure it is writable. See the diagnostic information available in **Custom Fields > Database Tables > Help** if you are having issues around this.

## Using a filter

If you prefer, you can use the following filter to modify the JSON directory:

```php
<?php
/*
 * Changes the ACF Custom Database Tables JSON directory.
 * This needs to run before the 'plugins_loaded' action hook, so 
 * you need to put this in a plugin.
 */
add_filter( 'acfcdt/json_dir', function ( $json_dir ) {
	return '/full/path/to/my-custom-json-directory';
} );
```

Again, this code needs to run before the plugins_loaded action hook fires, so this needs to go in a configuration plugin.