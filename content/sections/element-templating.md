---
category:
    - templating
title: "Element Templating"
date:  2017-11-20T10:17:50+01:00
weight: 5
url: /sections/templating/elements/
---

Elements are pieces of HTML that are not sections or columns. They're just needed as extra's. On this page you'll find all the elements used by Cuisine Sections. These templates can be overwritten in the following folder:

`/my-theme/elements/`

---

### Pagination



---

### Autoloader


---

### The Loader Element

If you have a collection column which you've configured to use endless-scroll as navigation, you'll see a loader pop-up every time you've reached the end of the collection. This means Cuisine Sections is busy fetching new posts to load. 

This loader is done completely in HTML and CSS, which is why we've created a simple template for it. <br/>

![The loader](/images/loader.png)<br/>

The overwritable location for these elements can't really be found in the UI of Cuisine Sections. Currently there is only one though, so for now we'll list any element templates here:

> /my-theme/elements/loader.php -> HTML for the loading indicator

