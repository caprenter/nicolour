<!-- Gallery -->
  {% assign festival_array = "" | split: ',' %}
  {% assign image_files = site.static_files | where: "image", true | reverse %}
  {% for image in image_files %}
    {% if image.name contains include.album" %}
        {% assign festival_array = festival_array | push: image %}
    {% endif %}
  {% endfor %}
<div class="gallery-credit"><p>Thanks to <a href="https://bingleycameraclub.co.uk/">Bingley Camera Club</a> for the photos.</p></div>
<div class="gallery">
{% for image in festival_array %}
{% assign indexmod3 = forloop.index | modulo: 3 %}
{% if indexmod3 == 1 %}<div class="row">{% endif %}
{% assign altcaptitle = image.basename | replace: "_"," " | append: " - Photos by Bingley Camera Club" %}
<a href="{{site.baseurl}}{{image.path}}" data-toggle="lightbox" data-gallery="example-gallery" data-caption="{{ altcaptitle }}" class="col-sm-4"><img src="{{site.baseurl}}{{image.path | replace: 'gallery','thumbnails'}}" alt="{{ altcaptitle }}" title="{{ altcaptitle }}" class="img-fluid" /></a>
{% if forloop.last %}</div>{% elsif indexmod3 == 0 %}</div>{% endif %}
{% endfor %}
</div><!-- Gallery -->  

