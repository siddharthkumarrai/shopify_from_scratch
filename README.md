# shopify_from_scratch
## Folder Structure
```terminal
mkdir assets, config, layout, locales, sections, snippets, templates
```
> Project
- assets
- config
- layout
- locales
- sections
- snippets
- templates

> assets/style.css.liquid

> assets/scripts.js.liquid

> layout/theme.liquid
```liquid
layout/theme.liquid

<!doctype html>
<html>
  <head>
    {{ content_for_header }}
    {{ 'style.css | asset_url | stylesheet_tag }}
  </head>
  <body>
      {{ content_for_layout }}

      {{ 'script.js' | asset_url | script_tag }}
  </body>
</html>
```
> templates/index.liquid
```liquid
<h1> hello i am siddharth kumar rai </h1>
```
> snippets/header.liquid
```liquid
<header>
    <h1> code with sidd </h1>
</header>
```
#### Render header.liquid
> layout/theme.liquid
```liquid
  <body>
      {% render 'header' % }}
      {{ content_for_layout }}
  </body>
```
> templates/index.liquid
```liquid
  <h1 class="text-center font-bold text-rose-400 my-16">{{ collections.frontpage.title }}</h1>
  {% for product in collections.frontpage.products %}
     <a href="{{ product.url }}">
    <li>
        <img
          src="{{ product.featured_image | image_url }}"
          alt="{{ product.title }}"
          width="200"
          height="200"
        >
        <h1>{{ product.title | link_to: product.url }}</h1>
        <h4>{{ product.description }}</h4>
        <h1>{{ product.price | money }}</h1>
    </li>
    </a>
  {% endfor %}





