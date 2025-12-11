---
layout: default
title: Nicolour Illustration
class: 'home-template'
navigation: True
#logo: /assets/images/splashes/Nicolour_workshop.2.JPG
current: home
#Use 'our_id' below for the next film to be shown. The id is in the csv file
# we use {% assign film = site.data.films | where:"our-id", page.our-id | first  %}
# in _includes/head.html to make use of the data below using e.g. film.main-image
# Defaults to use if no 'next film'
cover: splashes/Nicolour_workshop.2.JPG
---
<!-- < default -->
<!-- The tag above means - insert everything in this file into the [body] of the default.hbs template -->
<!-- The big featured header  -->
<header class="main-header" style="background-image: linear-gradient(rgba(0, 0, 0, 0),rgba(0, 0, 0, 0.1)), url({{ site.baseurl }}/assets/images/{{ page.cover }}); background-position-y:0">

<a class="scroll-down icon-arrow-left" href="#content" data-offset="-45"><span class="hidden">Scroll Down</span></a>

</header>

<!-- The main content area on the homepage -->
<main id="content" class="content" role="main" markdown="1">
{% include main.md %}

</main>
