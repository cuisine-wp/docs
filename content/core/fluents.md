---
category:
- utilities
title: "Fluents"
date: 2017-11-15T22:48:32+01:00
weight: 5
url: /core/utilities/fluents/
---

A fluent is an object where it's arguments are fluently settable. It's part of Cuisine's utility classes and it's mainly meant to be extended. You can find it here:

`Use Cuisine\Utilities\Fluent`

---

## Extending Fluents:
Fluents are meant to be extended for any object that needs easy assignable / fetchable properties. Here's an example:

```php

class Person extends \Cuisine\Utilities\Fluent{}

$person = new Person([ 'firstName' => 'John', 'lastName' => 'Doe' ]);

echo $person->get('firstName');

```
This example creates a new Person class. The class can be populated by key-value properties. A property can then be fetched using the <ins>get()</ins> method. 

### Setting data
Each argument you pass along is settable by calling it as a function:

```php
$person->firstName = 'Jane'
echo $person->get('firstName').' '.$person->get('lastName'); // Jane Doe
```
This example changes the first name we've set in our previous example.

---

## Data formats
A fluent can return your data (or the entire object) in a few formats:

### toArray()
Returns the Fluent as a key-value array
```php
var_dump( $person->toArray() );
```

### toJson()
Returns the Fluent as a key-value json string:
```php
$string = $person->toJson();
```

