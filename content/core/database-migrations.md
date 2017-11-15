---
categories:
- database
title: "Database Migrations"
date:  2017-11-15T22:33:51+01:00
weight: 5
url: /core/database/database-migrations 
---

Custom database tables in WordPress are usually a hassle of checking if it exists already. Apart from that it's not very database agnostic. Cuisine tries to fix this by, basically, implementing [Laravel's native migration system](https://laravel.com/docs/5.5/migrations).

---

## Getting started

Creating database migrations with the power of Cuisine is quite easy; 
you just create a class that extends

\Cuisine\Database\Migrations\Migration;
And use WP Cli to run the command:

wp cuisine migrate
That's it! See our examples for more:

---

### Creating and dropping custom tables

This actually looks exactly the same as Laravel's database migrations, with the exception of having to extend a different class and create an instance of that class at the bottom.

    namespace MyPlugin\Database;

    use Cuisine\Wrappers\Schema;
    use Cuisine\Database\Blueprint;
    use Cuisine\Database\Migrations\Migration;

    class ProductMetaMigration extends Migration{


        /**
        * Put the table up
        *
        * @return void
        */
        public function up()
        {
            Schema::create( 'product_meta', function( Blueprint $table ){
                $table->increments( 'id' )->unique();
                $table->integer( 'product_id' )->unsigned();
                $table->string( 'image_url' )->nullable();
                $table->integer( 'position' );
                $table->float( 'price' );
                $table->integer( 'stock' );
            });         
        }

        /**
        * Default down function
        *
        * @return void
        */
        public function down()
        {
            Schema::drop( 'product_meta' );
        }

    }


    \MyPlugin\Database\ProductMetaMigration::getInstance();

In this example a table named product_meta is created or destroyed, depending on which direction the migration is running.

---

### Creating columns

You can create a lot of different column types with Cuisine. Here's a list:

| Command | Description |
|---------|-------------|
| $table->bigInteger('votes'); | BIGINT equivalent for the database. |
| $table->binary('data');  | BLOB equivalent for the database. |
| $table->boolean('confirmed'); | BOOLEAN equivalent for the database. |
| $table->char('name', 4); | CHAR equivalent with a length. |
| $table->date('created_at'); | DATE equivalent for the database. |
| $table->dateTime('created_at'); | DATETIME equivalent for the database. |
| $table->decimal('amount', 5, 2); | DECIMAL equivalent with a precision and scale. |
| $table->double('column', 15, 8); | DOUBLE equivalent with precision, 15 digits in total and 8 after the decimal point. |
| $table->float('amount', 8, 2); | FLOAT equivalent for the database, 8 digits in total and 2 after the decimal point. |
| $table->increments('id'); } Incrementing ID (primary key) using a "UNSIGNED INTEGER" equivalent. |
| $table->integer('votes'); | INTEGER equivalent for the database. |
| $table->longText('description'); | LONGTEXT equivalent for the database. |
| $table->mediumInteger('numbers'); | MEDIUMINT equivalent for the database. |
| $table->mediumText('description'); | MEDIUMTEXT equivalent for the database. |
| $table->smallInteger('votes'); | SMALLINT equivalent for the database. |
| $table->string('email'); | VARCHAR equivalent column. |
| $table->string('name', 100); | VARCHAR equivalent with a length. |
| $table->text('description'); | TEXT equivalent for the database. |
| $table->time('sunrise'); | TIME equivalent for the database. |
| $table->tinyInteger('numbers'); | TINYINT equivalent for the database. |
| $table->timestamp('added_on'); | TIMESTAMP equivalent for the database. |

---

### Saving & Fetching data
WordPress has all sorts of functions for saving and retrieving your data from the 12 database tables it already knows. We wouldn't want to leave you hanging, so we created a simple wrapper for your custom tables as well.

```php

use Cuisine\Wrappers\Record;

//inserting:
Record::insert( 'product_meta', $data );

//updating:
Record::update( 'product_meta', $id, $data );

//removing:
Record::delete( 'product_meta', $id );

```

The record class can handle table inserts, updates and upserts, but also fetches:

```php

//find all product meta associated with this product:
Record::find( 'product_meta' )
        ->where(['product_id' => $product_id ])
        ->results();

//find the first product meta where the price is 0
Record::find( 'product_meta' )
        ->where([

            'product_id' => $product_id,
            'price' => 0

        ])->first();
```

Adding WHERE clauses results in "AND" queries by default. Currently we're still working on "OR" support.

`Record::find()` queries will return either an `Array` or `null` if the query returned no table rows.



