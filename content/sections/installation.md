---
category: 
    - 'getting-started'
title: "Installation"
date:  2017-11-18T09:02:51+01:00
weight: 5
url: '/sections/getting-started/installation/'
---

Clone the git repo - `git clone git@github.com:cuisine-wp/chef-sections.git` or install with composer:

`composer require cuisine-wp/cuisine-sections`

Composer will bring Cuisine Section's dependency, which is Cuisine Core into your project as well. If you've installed using git, please also install cuisine core manually by cloning Cuisine Core's git repo as well: `git clone https://github.com/cuisine-wp/cuisine.git`

After you have all the files you need you can install both Core and Sections as regular WordPress plugins:

1. move the files to wp-content/plugins (or your custom plugin folder)
2. get into the WordPress admin and go to plugins
3. activate Cuisine Core
4. activate Cuisine Sections

---

### Getting Started

On default, Cuisine Sections removes the WordPress wysiwyg editor for pages and exchanges it for the sections builder. You can now easily create new sections with the columns of your choice. To add a sections layout to any other post type, [please check the documentation on adding sections to post types](/sections/getting-started/adding-section-post-types/).