<div class="col mb-4">
  <div class="card h-100">
  <div class="card-header {{ service.color }}">
    <h4 class="service-title"><a href="{{ service.slug }}">{{ service.name }}</a></h4>
  </div>
      <a href="{{ service.slug }}"><img class="card-img-top p-0" src="assets/images/splashes/{{ service.image }}" alt="{{ service.alt-text }}"/></a>
    <!--<h2 class="blog"><a href="{{ post.url }}">{{ post.title }}</a></h2>
    <p>{{ post.date | date_to_string }}</p>-->
    <div class="card-body">
      <p class="card-text m-0">{{ service.short-description | markdownify | strip_html | markdownify }}</p>
    </div>
  </div>
</div>