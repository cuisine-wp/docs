---
title: Changelog
url: /changelog/
---

### 3.0.0
__2017-07-14__

* Compatibility with Sections & Forms 3.0
* Database migrations added
* Cron job api added
* Adds a flex field
* Repeater field fixes
* Settingspages can now have editors
* Create top-level admin menus
* A lot of minor bugfixes

### 1.6.3
__2016-11-29__

* Added a WP Cron extension
* Added the option of showing settings tabs in SettingsPages
* Fixes RepeaterField issues with positions
* Minor bugfixes

### 1.6.2
__2016-10-06__

* Major template revision:
* * Page / Post-type templates now reside in /pages
* * Views folder is gone
* Support for ignoring the Cuisine sass pipeline
* Added cache-busting to Cuisine's require
* Added shim-support to Cuisine's require
* Various repeater-field bugfixes
* Allow SVG uploads in MediaField (thanks to @corjen)
* Minor bugfixes


### 1.6.1
__2016-06-27__

* Compatibility release for the new Sections & Forms
* Fixed language issues
* Fixed a schema.org shortcode bug
* Minor bugfixes



### 1.6.0
__2016-05-06__

* Support for schema.org added
* Fix for multiple media-fields on a single page
* Fix for 404-template finding
* Post type labels updated to coincide with WP 4.5
* Repeater-field fixes for underscore 1.7
* Minor bugfixes



### 1.5.9
__2016-04-26__

* Updated the Twitter share-url
* Support for international zipcode validation
* Admin-fields now trigger a "refreshField"-event
* Readme & changelog fixes
* Fields don't check post_meta anymore
* Minor bugfixes



### 1.5.8
__2016-03-02__

* Updated the Taxonomy utility to coincide with PostType.
* Sorting bug fixed
* MetaboxBuilder more extendable
* Bugfixes to Field-controller in JS
* Minor bugfixes.



### 1.5.7
__2016-02-12__

* Added a Logger
* Update to RepeaterFields: they can now provide a cut-and-dry array of field-values on saving.
* Big (breaking) fixes to Editor field handling
* Field engine update (classes & validation)
* Bugfix for the SettingsPageBuilder when no parent was set.
* Minor bugfixes.


### 1.5.6
__2016-01-25__

* Fontawesome updated to 4.5
* Custom submenu pages support added for the SettingsPage class
* Added support for objects in Sort::byField
* Refactored Relative dates
* Bugfix for the datepicker ui
* Minor bugfixes.


### 1.5.5
__2015-12-21__

* Date-picker support to the datefield added
* Added a RootPostId function to the session class, to get the post ID from $wp_the_query
* Adds easy access to User attributes
* Lots of other little improvements to the User class
* Script::analytics now works with the modern ga notation
* Minor bugfixes.


### 1.5.4
__2015-11-25__

* Added the option to pass parameters to templates
* Browsersync support for requirejs
* Taxonomy highlighting in the Nav class
* Session crawler checker added
* Added a new "File" field-type
* Bugfix to the field-class system.
* Minor bugfixes.


### 1.5.3
__2015-10-05__

* Checkboxes choice-fields support added
* Support for editor-fields in repeater fields added.
* Slug validation to the Validate class added.
* Chef Related template-support added.
* Field classes bugfix when there's no defaul value.
* Bugfix in script-autoloaded.
* Minor bugfixes.


### 1.5.2
__2015-09-08__

* Padding dropdown error fixed.
* Removing an image with an image field
* Removed an Exception error in Image.php


### 1.5.1
__2015-08-20__

* Added page-template support to the template-engine
* Added a fresh-forms wp cli command
* Added a getProperty method for Fields
* Added the ability to create SettingsPages
* Minor bugfixes


### 1.5.0
__2015-08-12__

* Added the Date Utility class
* Added the Number Utility class
* Added single-post pagination
* Added a save-field filter
* Fixes to the repeaterfield when saving with ajax
* Fixes a routing error in the template engine


### 1.4.9
__2015-08-11__

* Added the Template::section selector
* Added Date-field support
* Fixed some big pagination bugs
* Minor bugfixes


### 1.4.8
__2015-08-06__

* Added Nav active-state setting
* Added SVG upload support
* Minor bugfixes


### 1.4.7
__2015-08-05__

* Editor hotfix; the value remained empty
* Added WP CLI support for Sass-refreshing


### 1.4.6
__2015-08-03__

* Repeaterfield fixes
* Media Library incremental IDs

### 1.4.5
__2015-07-28__

* Big media-library update
* Filter for scripts added
* Some more editor bugfixes
* Saving single checkboxes who are not checked
* Added a simple template-finder
* Added some more JS vars
* Fixes to the current user variable



### 1.4.4
__2015-07-07__

* Mobile Nav support
* Json validation added
* Fontawesome shortcut added
* Calling single sections from the Loop class
* Fix for the media-library when no thumbnail is set


### 1.4.3
__2015-07-03__

* Editor refreshing fixes
* Readme updates
* Media library bugfixes


### 1.4.2
__2015-07-02__

* Refreshing WP editors from javascript bugfix


### 1.4.2
__2015-06-30__

* First public release
