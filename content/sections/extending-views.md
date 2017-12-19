---
category:
    - extending
title: "Extending section views"
date:  2017-11-20T10:17:50+01:00
weight: 5
url: /sections/extending/views/
---

Views in Sections are just the devisions in columns. You'll recognise them by these icons:
![Section views](/images/section-views.png)
Currently there are six different views, selectable for each section:

- Fullwidth
- Half / half
- Sidebar left
- Sidebar right.
- Three columns
- Four columns

---

## Adding a new view

Adding a new view can be done by using a filter, which uses a key => value structure. The key (in this case) is the name (and subsequently the css class) of the view and the value is the amount of columns that need to be rendered. Consider this example:

```php
add_filter('cuisine_sections_section_views', function( $views ){
    $views['bar-wide-bar'] = 3;
    $views['wide-bar-bar'] = 3;
    return $views;
});
```
This example adds two new views to chose from, where we have a wide column and then two smaller 'bar' columns. This will result in two new icons, which will default to displaying the amount of columns. If you want to change the icons, you'll have to add some CSS to your WordPress admin:

```css
.section-wrapper .section-controls .radio > span.bar-wide-bar{
  background: url("../images/bar-wide-bar.png");
}
.section-wrapper .section-controls .radio > span.wide-bar-bar{
  background: url("../images/wide-bar-bar.png");
}
```