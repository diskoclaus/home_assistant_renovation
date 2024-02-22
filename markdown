&nbsp;<ha-icon icon="mdi:trash-can"></ha-icon> {{ state_attr('sensor.dagsrenovation', 'tekst') }} afhentes {{ states('sensor.dagsrenovation') }}&nbsp;

{% set ns = namespace(found=false,name='') %}

{% set sorted_renovation = states.sensor.dagsrenovation.attributes.fremtidig_afhentning | sort(attribute='next_in_days') %}
{% set img_size = "50" %}
{% for renovation in sorted_renovation %}
   {% set ns.found = true %}
     {% set ns.firstname = renovation %}
{% endfor %}
    {% set img1 = "&nbsp;" %}
    {% set img2 = "&nbsp;" %}
{% if ns.found==true -%}
    <table width='100%' border='0'>
    <thead>
{% for renovation in sorted_renovation %}
  {% set my_entity = renovation.name %}

  {% if my_entity == 'Pap/papir' %}
    {% set img1 = "<img src='https://website.dk/local/img/reno_pap.webp' height='" ~ img_size ~ "'>" %}
    {% set img2 = "<img src='https://website.dk/local/img/reno_pappapir.webp' height='" ~ img_size ~ "'>" %}  
  {% elif my_entity == 'Rest/mad' %}
    {% set img1 = "<img src='https://website.dk/local/img/reno_restaffald.webp' height='" ~ img_size ~ "'>" %}
    {% set img2 = "<img src='https://website.dk/local/img/reno_madaffald.webp' height='" ~ img_size ~ "'>" %}  
  {% elif my_entity == 'Glas/metal' %}
    {% set img1 = "<img src='https://website.dk/local/img/reno_flasker.webp' height='" ~ img_size ~ "'>" %}
    {% set img2 = "<img src='https://website.dk/local/img/reno_metal.webp' height='" ~ img_size ~ "'>" %}
  {% elif my_entity == 'Farligt affald' %}
    {% set img1 = "<img src='https://website.dk/local/img/reno_farligtaffald.webp' height='" ~ img_size ~ "'>" %}
    {% set img2 = "&nbsp;" %}  
  {% elif my_entity == 'Tekstiler' %}
    {% set img1 = "<img src='https://website.dk/local/img/reno_tekstiler.png' height='" ~ img_size ~ "'>" %}
  {% endif %}

<tr><td>{{ img1 }}</td><td>{{ img2 }}</td><td>&nbsp;&nbsp;{{
renovation.name }} - {{ renovation.title }}</td>{% endfor %}</tr></thead><tbody></table>

{% endif -%}   &nbsp;          
