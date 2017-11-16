---
category:
- utilities
title: "Collections"
date:  2017-11-15T22:48:27+01:00
url: /core/utilities/collections
---

Collections are souped-up arrays. It's purpose is to work more fluently with large datasets and keep your code more readable. It's very much modelled after [Laravel's base collection](https://laravel.com/docs/5.5/collections).

Collections are available through Cuisine's wrapper system. You can include it's class like this:

`use Cuisine\Wrappers\Collection`

---

## Creating collections

Using the <ins>Collection</ins> facade, you can easily create collection from any array, like so:

```php
$collection = Collection::make([ 1, 2, 3 ]);
```

---

## Return values
A collection uses a return value to determine what to return. In a default collection this takes just two forms:

### toArray()
```php 
$items = $collection->toArray()->all();
```
This example turns the collection into an array and then gives all items back with the <ins>all()</ins> method.

### toJson()
```php
$json = $collection->toJson()->all();
```
This example sets the returnValue to json and then returns all items as a (you guessed it) json string.

---

## Available methods

### All()
Returns all items, in the set return value (defaults to array)

```php
$allItems = $collection->all();
```

### Get( $key, $default = null )
Returns a single item out of the collection. If the key can't be found, it returns the default value passed in the second parameter.

```php
$singleItem = $collection->get( $key, 'defaultValue' );
```

### First()
Returns the first value of a collection:

```php
$firstValue = $collection->first();
```

### isEmpty()
Returns a boolean on wether or not this collection is empty

```php
if( $collection->isEmpty() ) echo 'empty collection!';
```

### Count()
Returns the amount of items as an integer

```php
$amount = $collection->count();
```




