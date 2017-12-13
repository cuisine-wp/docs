---
category: 
    - templating
title: "Templating Containers"
date:  2017-11-26T14:23:56+01:00
weight: 5
url: /sections/templating/containers
---

Section containers (surprise) contain other sections. They can be fully templated though, so If you'd like to create tabs to switch between the sections in the container, you can.

Containers use the same [template hierarchy](/sections/templating/sections/) as regular sections, with one exception: containered sections don't have a view-type (fullscreen, half-half or )

1. /my-theme/sections/{post-slug}-{section name}.php
2. /my-theme/sections/{post-slug}-{section view}.php
3. /my-theme/sections/{section view}.php
4. /my-theme/sections/default.php

the big difference for a container would be in the view. It's a container, so it doesn't have any information on how many columns it would contain.  Here's the same hierarchy for a container:

1. /my-theme/sections/{post-slug}-{section name}.php
2. /my-theme/sections/{post-slug}-{container type}.php
3. /my-theme/sections/{container type}.php
4. /my-theme/sections/container.php

Here we can notice two things: the last template isn't <ins>default.php</ins> but <ins>container.php</ins>.

## Container Types

