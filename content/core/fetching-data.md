---
categories:
- database
title: "Fetching Data"
date:  2017-11-15T23:07:48+01:00
url: /core/database/fetching-data/
---

WordPress has all sorts of functions for saving and retrieving your data from the 12 database tables it already knows, but since we now can easily [create new database tables with Database Migrations](/core/database/migrations), we need a new way of fetching your data. 

In Cuisine we do this with the Record class, which is [available through Cuisine's wrapper system](/core/getting-started/structure/). Just include the following namespace:

`use Cuisine\Wrappers\Record`

---

## Fetching a single record:

```php
$id = '1';
Record::get( 'product_meta', $id );
```
We tell the record class to go and fetch the product_meta with an ID of 1. 
This will return a stdObject with your data.

### Fetching a single record with a more complext query

If you want to look for a record that you don't know the ID of, you can use the `find` method, which we'll also use to fetch multiple records in later examples. For now, here's how you get a single record:

```php
$productId = '1';
Record::find( 'product_meta' )->where( 'product_id', $productId )->first();
```
As you can see all of these methods are chainable, which makes this query very easy to read. This will return the first record it finds where the <ins>product_id</ins> is equal to <ins>$productId</ins>.

--- 

## Fetching mutliple records:

```php
$meta = Record::find( 'product_meta' )
        ->where(['product_id' => $product_id ])
        ->results();

$metaArray = $meta->toArray();

```

In this example we'll get all records in the <ins>product_meta</ins> table that belong to our <ins>$product_id</ins> variable. The results will be a [Cuisine Collection](/core/utilities/collections), which you can easily convert to an array, a json string or whatever you fancy.

### Adding multiple clauses.
You may have noticed that the where method takes an array as it's parameter. In this array we can of course put multiple clauses. Like so:

```php
Record::find( 'product_meta' )
        ->where([

            'product_id' => $product_id,
            'price' => 0

        ])->results();
```
This example will return a collection of product meta where the price is zero.

>*Important to know:* 
>Adding WHERE clauses results in "AND" queries by default. Currently we're still working on "OR" support.
>
>`Record::find()` queries will return either an `Array` or `null` if the query returned no table rows.
>


