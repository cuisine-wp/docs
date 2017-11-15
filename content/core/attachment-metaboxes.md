---
title: "Attachment Metaboxes"
date: 2017-11-15T14:05:24+01:00
weight: 5
url: /core/admin/attachment-metaboxes/
---

Attachments in WordPress do sometimes require some extra meta-data. In Cuisine, creating custom fields for attachments becomes an extremely easy task. Just like our other metaboxes, the Attachment-Metabox object can take an array of [field-objects](/fields/using-fields/) which are validated and saved automatically.

The Metabox class is available through [Cuisine's Wrapper System](/getting-started/structure/), so you can start using it by adding

`use Cuisine\Wrappers\AttachmentMetabox`

to the top of your php-document.

---


### Creating an Attachment Metabox

Creating a new attachment metabox with a few custom fields is fairy straightforward. Let's look at an example:

{{< highlight php >}}

$fields = array(
	Field::text( 'name', 'Label' ),
	Field::text( 'name-2', 'Label' )
);

AttachmentMetabox::make()->set( $fields );

{{< / highlight >}}  

<br/>

In contrast to our other metabox classes, you don't have to provide a title or slug for this metabox, since attachments don't really display custom fields in seperate boxes. Let's break down the code above anyway:

>**AttachmentMetabox::make()** is the function we use to prop up our Metabox. **set()** actually registers it with WordPress. It takes an array of [Field Objects](/fields/using-fields/).
