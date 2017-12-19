---
category: 
    - 'getting-started'
title: "Changelog"
date:  2017-11-18T09:02:51+01:00
weight: 5
url: '/forms/getting-started/changelog/'
---



### 2.2.0 2017-03-06

* Added support for redirect after submit
* Added fully extenable settings panels 
* Added support for Google tag manager
* Fixes to notification system in compatibility with other plugins
* Various compatibility issues fixed with the FormBuilder
* Minor fixes



### 2.1.9 2016-11-29

* Compatibility release for Chef Payment & Chef Invoices
* Extendability increased
* Form rendering is now optional when invoking the Form object
* Various compatibility issues fixed with the FormBuilder
* Firefox lightbox bug fixed
* Minor fixes


### 2.1.8 2016-10-06

* Added support for ignoring the sass-pipeline
* Notification fixes
* Support for the multipage form plugin
* File field errors fixed
* Minor fixes

### 2.1.7 2016-06-27

* Completely new UI
* Support for fields in rows
* Translated into english
* Escaping all output
* Added a shortcode
* Antispam honeypot added
* International zipcode validation
* Minor fixes

### 2.1.6 2016-04-25

* Support for password fields
* Bugfix for switching field positions
* Changed some private functions to protected for extendability
* Added user-meta support in tags.
* Fixes to spam
* Minor styling fix to checkboxes


### 2.1.5 2016-03-24

* Added a wysiwyg field
* Added entry-mapping as a default feature
* Notifications are a bit wider
* Bugs in multi-select fields are fixed
* Checkboxes get there own class
* Cleaned up the entry-manager in admin: every field uses the notification-function
* File-fields are now stored as part of the entry.
* Minor styling fix to checkboxes



### 2.1.4 2016-02-12

* Added the HTML and Break fields
* Added new number validation
* Added more actions and filters for fields
* Fixes for the Notification and Settingsmanager Editor-fields with Cuisine.
* Only validate non-empty fields now
* Tag refactoring: post, postmeta, user and usermeta
* Minor styling fix to checkboxes



### 2.1.3 2016-01-15

* Non JS form-submitting
* Added support for file-uploads
* Added support for tab-indexing
* Added support for entry pagination
* Added loads of actions and filters to the Form class in PHP and JS
* Fixes an issue where confirmation-messages where static
* Fixes SMTP access to Mandrill
* Minor styling fix to checkboxes



### 2.1.2 2015-12-22

* Added loads of filters and actions to make forms more flexible
* Added a messages object so plugins can inject (error)messages to forms.
* Added form message styling
* Fixed a bug where arbitrary html elements with .form classes threw a JS error.
* Minor styling fix to checkboxes



### 2.1.1 2015-12-09

* Entries are filterable now
* Form::get refactored to work with the existingForms variable
* Added support for no notifications
* Added password field support
* Form and field classes are now properly filterable
* The defaulValue of a field is now filterable before and after Tags
* Custom validation support
* Minor bugfixes.



### 2.1.0 2015-11-25

* Datefields are working on the front-end now
* Big formbuilder fixes. Also fetching corresponding form-ids
* New deletable-boolean added to fields.
* The Entry class is now extendable and filterable.
* The Notification class is now extendable and filterable.
* Notification values can now contain post-meta tags.
* Some code-cleanup and styling fixes
* Various bugfixes to multifields
* Minor bugfixes.



### 2.0.9 2015-11-12

* Added support for form-redirecting
* Added persistent session-storage for redirecting
* Added support for max entries
* Added support for validity between dates
* Validation Errors are now overwritable as a Cuisine JS-var
* Added {{ entry_id }}-tag to notifications
* Minor bugfixes.



### 2.0.8 2015-10-25

* Added Tag support in notifications
* Added Address-field validation
* Added the option of overwriting the Notification HTML by template.
* Each field-class can now submit their own html to a notification
* Fixed a bug where confirmation messages weren't being saved.
* Minor bugfixes.


### 2.0.7 2015-09-30

* Fixes textarea validation
* Adds tag-support for hidden fields.
* Address-fields done neatly
* Address-field styling
* Minor bugfixes.



### 2.0.6 2015-09-16

* Added the ability to submit the form from outside Form.js
* Fixes address validation
* Fixes non-required validation
* Fixes the column just displaying the last 5 forms.
* Fixes checkboxes fields, which were not displaying properly
* Minor bugfixes.



### 2.0.5 2015-09-09

* Added an address field-type.
* Added getters for the form-object.
* Fixed a bug with field labels
* Fixed a bug where choicefields rendered the wrong options
* Minor bugfixes.



### 2.0.4 2015-08-17

* Added a formbuilder for adding forms through code
* Added button-filters
* Changed the namespaces of builders, to better reflect what they do
* Minor bugfixes.


### 2.0.3 2015-08-15

* Added a settingspage for Mandrill
* Added smart default-value tags
* Added flexible form-settings panels
* Further minor bugfixes


### 2.0.2 2015-08-05

* Sending via STMP with Mandrill
* Field validation bugfix
* Further minor bugfixes


### 2.0.1: 2015-07-10

* Notifications working
* Sending feedback
* Added a loader


### 2.0.0: 	2015-07-06

* First public release
