---
category: 
    - 'getting-started'
title: "Installation"
date:  2017-11-18T09:02:51+01:00
weight: 5
url: '/forms/getting-started/installation/'
---

Clone the git repo - `git clone git@github.com:cuisine-wp/cuisine-forms.git` or install with composer:

`composer require cuisine-wp/cuisine-forms`

Composer will bring Cuisine Forms' dependency, which is Cuisine Core into your project as well. If you've installed using git, please also install cuisine core manually by cloning Cuisine Core's git repo as well: `git clone https://github.com/cuisine-wp/cuisine.git`

After you have all the files you need you can install both Core and Forms as regular WordPress plugins:

1. move the files to wp-content/plugins (or your custom plugin folder)
2. get into the WordPress admin and go to plugins
3. activate Cuisine Core
4. activate Cuisine Forms
