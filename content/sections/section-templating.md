---
category:
    - templating
title: "Section Templating"
date:  2017-11-20T10:17:50+01:00
weight: 5
url: /sections/templating/sections/
---

Usually you won't need to change a section template. The default pretty much handles all logic, but if you feel the need to change this template you'll find the original here:

`plugins/cuisine-sections/Templates/Sections/default.php`

If you haven't yet, [read up on Cuisine Sections template structure & hierarchy](/sections/templates/introductios/). They'll help you immensly along the way

---

## Template hierarchy

Like in our columns, sections have a custom template hierarchy.

You'll be able to find which files you need to create in your theme by using the [Template Snitch](/sections/templates/introduction/) explained in the introduction. The template snitch will always follow this hierarchy:

1. /my-theme/sections/{post-slug}-{section name}.php
2. /my-theme/sections/{post-slug}-{section view}.php
3. /my-theme/sections/{section view}.php
3. /my-theme/sections/default.php

Sections will first be looking at a template the current section name that's also in a certain post. Read up on the Section Name property later in this article.

Then it'll check the section view type inside your current post. View types are what detirmen the eventual amount of columns in your section. Here are the available view types, along with each view-type slug which is what you need to use in your template name:

1. 100% (fullwidth)
2. 50% - 50% (half-half)
3. 30% - 70% (sidebar-left)
4. 70% - 30% (sidebar-right)
5. 33% - 33% - 33% (three-columns)
6. 25% - 25% - 25% - 25% (four-columns)

So if you have a page called home, and you wanted to add a piece of custom HTML to every three-column section, you could create a template called

`/my-theme/sections/home-three-columns.php`

and overwrite every three-column section on the homepage.

If the page specific and view-type specific file cannot be found it'll be looking for a general view-type file. If all of your fullwidth sections need a little custom html you could use

`/my-theme/sections/fullwidth.php`

And all fullwidth sections on the entire website will refer to this template. 

Finally we have the <ins>default.php</ins> file, which you can use to overwrite absolutely every section used on the website. This can be handy for certain layouts where you wish to inject stuff like extra schema.org data on a theme-wide basis.

---

## The Section Name

The section name can be set by WordPress administrators and refers directly to a sections template, anchor point and class. It's used -in short- to identify the section beyond it's ID and make it a little more recognizable in our code.

Section names can be editted by clicking the cog next to the Section Title input:<br/>
![Setting section names](/images/section-name.png)
<br/>
The screenshot above shows a fullwidth section which name is <ins>site-intro</ins>. This means it's most accurate custom template will be:

`my-theme/sections/{page_slug}-site-intro.php`

It will also mean that among <ins>section</ins> and <ins>fullwidth</ins>, it's class will contain <ins>site-intro</ins> as well. Dependent on if you are also using the Cuisine Section Navigation plugin, where you'll be able to skip from one section to the other, there will also be a `<span class="anchor" id="site-intro"></span>` element injected into your code.

