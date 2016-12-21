# Ostrichcize

**Contributors:** [tollmanz](https://profiles.wordpress.org/tollmanz/), [10up](https://profiles.wordpress.org/10up/)  
**Donate Link:** [http://wordpress.org](http://wordpress.org)  
**Tags:** debug, error reporting  
**Requires at least:** 3.3  
**Tested up to:** trunk  
**Stable tag:** 0.1.1  
**License:** GPLv2 or later  
**License URI:** [http://www.gnu.org/licenses/gpl-2.0.html](http://www.gnu.org/licenses/gpl-2.0.html)  

Hide PHP error reporting for specified plugins or the current theme.

## Description

Ostrichcize allows a plugin or theme developer to bury his or her head in the sand by turning off error reporting for 
select plugins or the current theme. This isn't something ostriches actually do, but many people think it is.

If you have ever installed a plugin or worked on a site with a plugin that throws numerous of errors and notices, but do
not have the time to fix the issue, you can turn off those notices with this plugin. By simply filtering the plugin, you
can add to the list of plugins for which no notices will be shown.

To add to this list simply write something like:

```php
function my_ostrichcized_plugins( $slugs ) {
	$slugs[] = 'debug-bar-cron';
	return $slugs;
}

function my_pre_my_ostrichcized_plugins() {
    add_filter( 'ostrichcized_plugins', 'my_ostrichcized_plugins' );
}

add_action( 'plugins_loaded', 'my_pre_my_ostrichcized_plugins', 1 );
```

Note that the filter must be added before any offending code is run in order to redefine the error reporting function
before it is first called. The means that in most cases, this code will need to run from a plugin and not a theme.

To turn off PHP error reporting for a theme, run:

```php
function my_ostrichcize_theme() {
    add_filter( 'ostrichcize_theme', '__return_true' );
}
add_action( 'plugins_loaded', 'my_ostrichcize_theme', 1 );
```

* Thanks to [Jeremy Felt](https://github.com/jeremyfelt) for assistance naming the plugin!
* Thanks to [Jeremy Clarke](https://github.com/jeremyclarke) for improving the Ostrich to work better with certain MU plugin scenarios.

## Installation

1. Install Ostrichcize if not already installed ([http://wordpress.org/extend/plugins/ostrichcize/](http://wordpress.org/extend/plugins/ostrichcize/))
2. Activate the plugin through the 'Plugins' menu in WordPress
3. Setup Ostrichcize rules as noted above

## Frequently Asked Questions

#### Is there a UI to add ostrichcize rules?

No. At this time, I really only want developer's using this tool. Any WordPress developer that is messing with error
handling should easily be able to make this plugin work. If not, the developer should not be using this tool. Similarly,
users should not be messing with error reporting.

#### Can I run this in production?

You certainly can, but that is not the intent of the tool. It is best to only run this in development.

#### What is the use case?

This plugin is inspired by having installed countless plugins that throw error notices. Many times, these are small,
non-critical errors. Since I often do not have time to fix the errors myself, I allow them to continue to muck up my
error logs or on screen display of errors. I thought it would be nice to have a way to hide these errors so that only
errors due to my custom code are displayed. Ostrichcize allows you to do just that.

## Changelog

= 0.1.1 =
* Load plugin on `'muplugins_loaded'`
* Only instantiate the Ostrich if an Ostrichcize filter is used

= 0.1 =
* Initial release
