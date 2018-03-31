# Shopify work
As a freelancer who sets up Shopify e-commerce stores, my clients sometimes request features outside of Shopify's default functionality. Thus, I often have to code a solution using Liquid. This repository holds the code customizations I've written for Shopify.

## Clients
### Kilari Blue ([kilariblue.com](www.kilariblue.com))
#### About
Kilari Blue is an online retailer that focuses on providing business casual and professional clothing for women. Our store carries mid-to-high end brands and designers who  provide a contemporary take on traditional business wear. The goal is to bring the unique pieces of boutiques into the workplace, but still staying within the office appropriate guidelines. Our customer is a young, fun, and trendy girl who is bored of wearing the same 5 basics to work and is looking for special, premium pieces that are more exciting than what she can find at department stores.
#### Requested feature
One aspect of Kilari Blue's brand is the styling of full outfits. For example, a customer looking for business casual outfits can simply view the "Biz Casual" collection and view an entire assemblage of full business casual outfits. The feature requested was to display the individual products in each outfit and allow the customer to buy them while on the full outfit product page.
#### Challenges
This is the first time I've worked with Shopify, but I'm familiar with e-commerce platforms as a whole because I've worked with Wordpress (as an intern at Bellanove ([bellanove.com](http://www.bellanove.com/))) and Squarespace (as CTO of Vanth ([vanththeapp.com](https://www.vanththeapp.com/))). However, it was clear that this requested feature would require some coding. Shopify uses a templating language called Liquid, and in fact, all Shopify themes use Liquid to build and put together page templates. I'd never worked with Liquid before, so the challenge was to figure out how to organize all the products (invididual products and full outfits) and collections, get an intuition for Liquid by reading its reference and documentation, and modify the product template to get the feature the client requested.
I also found that the feature itself also lent itself to other modifications the e-commerce store required. For example, the price of the full outfits had to be set to $0, which would be awkward to display. Thus, I had to make further code changes to hide the $0 pricing on collection and product pages. Furthermore, I also had to apply the requested feature to the quick view, since the quick view has to match the product page.
#### Theme
This Shopify store uses the [Icon theme](https://themes.shopify.com/themes/icon/styles/dolce?page=2#Reviews).
#### Code
I modified the [`product.customizable.liquid`](https://github.com/AmyJZhao/Shopify-Work/blob/master/product.customizable.liquid) file so that regular individual products could use the regular product template and the full outfits would use the customizable template.

To display the individual products in each outfit: 

I created a collection that would have the same handle as the product (so 'Timeless' collection for the 'Timeless' full outfit) and added the individual products to it. Then, in the `product.customizable.liquid` file, I added a loop that would iterate through all the products in the collection and display their details, prices, variants, and add to cart buttons.
``` liquid
<div id="product-right" class="desktop-6 mobile-3">
    <div id="product-description">
    ...
        {% assign collection_handle = product.handle %}
        {% for product in collections[collection_handle].products %}
            ...
        {% endfor %}
    ...
    </div>
</div>
```

I also modified the [`product.quick.liquid](https://github.com/AmyJZhao/Shopify-Work/blob/master/product.quick.liquid) file to display the list of individual products on Quick View as well.

This time, I needed the template to work for both regular products and full outfits. Thus, I wrote an if-else statement that would format the quick view based on the product type.
``` liquid
{% if product.type == 'Full Outfit' %}
    ...
    {% assign collection_handle = product.handle %}
    {% for product in collections[collection_handle].products %}
        ...
    {% endfor %}
    ...
{% else %}
    ...
{% endif %}
```