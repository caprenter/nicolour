<article class="post"> <!-- centres the content in the page -->
<section class="main-page">
<div markdown="1">

<div class="main">
  <div class="blog">     
  <div class="row row-cols-1 row-cols-lg-2 row-cols-md-2 row-cols-sm-2 d-flex align-items-stretch blog">
  {% for service in site.data.services %}   
    {% include card.md %}
  {% endfor %}
  </div>
  </div>
</div>

</div>
</section>
</article>