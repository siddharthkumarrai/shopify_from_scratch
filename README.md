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
```
> templates/product.liquid
```liquid
<img src="{{ product.featured_image | image_url }}" height="300px" width="300px">
<h1>{{ product.title }}</h1>
<h1>{{ product.price | money }}</h1>
<p>{{ product.description }}</p>

{% form 'product', product %}
  <select name="id">
    {% for variant in product.variants %}
      <option value="{{ variant.id }}">{{ variant.title }}</option>
    {% endfor %}
  </select>

  <button type="submit">Add to cart</button>
{% endform %}
```
> templates/cart.liquid
```liquid
{% form 'cart', cart %}
  <h1>Cart</h1>
  {% if cart.empty? %}
    <p>Cart is empty.</p>
  {% else %}
    {% for item in cart.items %}
      <div>
        <img src="{{ item.image | image_url: width:250  }}" height="300px" width="300px">
        <h2>{{ item.title }}</h2>
        <h1>{{ item.final_line_price | money }}</h1>
        <input name="updates[]" , value="{{ item.quantity }}">
        <a href="{{ item.url_to_remove }}">Remove</a>
      </div>
    {% endfor %}
    <button type="submit" name="update">
      updates
    </button>

    <br>
    <hr>
    <h3>Total Price : {{ cart.total_price | money }}</h3>
    <button type="submit" name="checkout">
      checkout
    </button>
  {% endif %}
{% endform %}
```




