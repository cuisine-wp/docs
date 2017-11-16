---
category:
- database
title: "Adding Updating Records"
date:  2017-11-16T20:41:20+01:00
weight: 5
url: /core/database/adding-updating/
---

Cuisine's Record class can be used to both [fetch data](/core/database/fetching-data/) and, as you will see, to update or delete data. This class was made to work together with custom tables you can add using [Cuisine's migration system](/core/database/migrations)

In Cuisine we do this with the Record class, which is [available through Cuisine's wrapper system](/core/getting-started/structure/). Just include the following namespace:

`use Cuisine\Wrappers\Record`

---

## Inserting data

Inserting data is as easy as this example:
```php
$productMetaId = Record::insert( 'product_meta', $args );
```
This example will create a new row in the 'product_meta' table and return this row's primary key.

If you make sure the array <ins>$args</ins> in this example is an exact key-value pair of your database table, everything will work out-of-the-box. If you've placed restrictions on your database table (like non-nullable fields) and you forget to include a key in your <ins>$args</ins> that can't be null, you'll get a MySQL error.


#### insertOrUpdate
Inserting data with or without a primary key can be done by using the <ins>insertOrUpdate()</ins> function. If there's no primary key given, a new record will be created. Here's an example:

```php
$args = [ 'id' => 1, 'price' => 100 ];
$productMeta = Record::insertOrUpdate( 'product_meta', $args );
```
This example will update a record with the ID of 1 and set it's price-field to 100.

---

## Updating
Updating a specific field is very easy, just include the row's primary key:

```php
Record::update( 'product_meta', 1, [ 'price' => 100 ]);
```
This function call will update the price of a row of product_meta with the primary key of 1.


