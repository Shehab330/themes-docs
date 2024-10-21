---
sidebar_position: 4
---

# Create your own funnel template

You can convert any HTML file into a funnel template by following these steps:

## 1. Create the HTML Structure

## 2. Add the necessary attributes to be replaced with the product information dynamically, combined with `data-vvveb-disabled`

### Add `checkout-form` id to render the checkout form

```html
<form data-vvveb-disabled id="checkout-form">
  // rest of the code remains the same
</form>
```

### Add `"x-checkout-btn` id to render the checkout button

:::info
The x-checkout-btn can be used without the `data-vvveb-disabled` attribute
:::

```html
<button id="x-checkout-btn">Buy Now - Cash on Delivery</button>
```

### Add `totalCost` id to render the total cost of the order

```html
<div>
  <span data-vvveb-disabled id="totalCost"> EGP2,254.33 </span>
</div>
```

### Add `price, salePrice, basePrice, discountPercent` ids to render the product's price and the variants of the product will render automatically

```html
<div data-vvveb-disabled id="price">
  <p id="salePrice">EGP100</p>
  <p id="basePrice">EGP150</p>
  <div class="percentage" id="discountPercent"><span> -40% </span></div>
</div>
```

### add `fixed-price, salePrice, basePrice, discountPercent` ids to render only the product's price

```html
<div data-vvveb-disabled id="price">
  <p id="salePrice">EGP100</p>
  <p id="basePrice">EGP150</p>
  <div class="percentage" id="discountPercent"><span> -40% </span></div>
</div>
```

### Add `x-bundles-title` id to render the bundle section title

```html
<div data-vvveb-disabled id="x-bundles-title">
  // rest of the code remains the same
</div>
```

### Add `x-bundles` id to render the bundle section

```html
<div data-vvveb-disabled id="x-bundles">
  // rest of the code remains the same
</div>
```

### Render the product's images in the carousel

#### create a div with the id `carouselExampleIndicators`

```html
<div
  id="carouselExampleIndicators"
  data-vvveb-disabled
  data-ride="carousel"
></div>
```

#### create a script tag with the id `gallery-template` as following

```html
<script id="gallery-template" type="text/html">
  <div class="carousel-container">
    {{# slides}}
    <div class="carousel-item {{#isFirst}} active {{/isFirst}}">
      <img class="d-block w-100" src="{{url}}" alt="" />
    </div>
    {{/ slides}}
  </div>

  <div>
    <ol class="thumbnails-container">
      {{# slides}}
      <li
        data-bs-target="#carouselExampleIndicators"
        data-bs-slide-to="{{index}}"
        class=" {{#isFirst}} active {{/isFirst}} thumbnail-item"
      >
        <img class="d-block object-fit-cover" src="{{url}}" alt="" />
      </li>
      {{/ slides}}
    </ol>
  </div>
</script>
```

#### the final HTML structure should look like this

```html
<div>
  <div
    id="carouselExampleIndicators"
    data-vvveb-disabled
    data-ride="carousel"
  ></div>

  <script id="gallery-template" type="text/html">
    <div class="carousel-container">
      {{# slides}}
      <div class="carousel-item {{#isFirst}} active {{/isFirst}}">
        <img class="d-block w-100" src="{{url}}" alt="" />
      </div>
      {{/ slides}}
    </div>

    <div>
      <ol class="thumbnails-container">
        {{# slides}}
        <li
          data-bs-target="#carouselExampleIndicators"
          data-bs-slide-to="{{index}}"
          class=" {{#isFirst}} active {{/isFirst}} thumbnail-item"
        >
          <img class="d-block object-fit-cover" src="{{url}}" alt="" />
        </li>
        {{/ slides}}
      </ol>
    </div>
  </script>
</div>
```

:::info
It will be replaced with the product's images automatically
:::

:::info
use the `carousel-container` class to style the carousel and the `carousel-item` class to style the carousel-item.
:::
:::info
You can use `thumbnails-container` class to style the thumbnails container and the `thumbnail-item` class to style the thumbnails.
:::
:::info
The classes provided are for demonstration purposes only. Feel free to use any classes you prefer, but ensure the specified IDs remain unchanged.
:::

## 3. Add the necessary scripts to the HTML file

```html
<!-- Vendor JS Files -->
<script src="https://files.easy-orders.net/funnels-assets/souq/assets/vendor/bootstrap/js/bootstrap.bundle.min.js"></script>
<script src="https://files.easy-orders.net/funnels-assets/souq/assets/vendor/swiper/swiper-bundle.min.js"></script>
<!-- Template Main JS File -->
<script src="https://files.easy-orders.net/funnels-assets/souq/assets/js/main.js"></script>
<!-- header timer -->
<script src="https://files.easy-orders.net/funnels-assets/souq/assets/js/timer.js"></script>
<!-- jquery -->
<script
  src="https://code.jquery.com/jquery-3.7.1.js"
  integrity="sha256-eKhayi8LEQwp4NKxN+CfCh+3qOVUtJn3QNZ0TciWLP4="
  crossorigin="anonymous"
></script>

<!-- fade-up animation [aos] -->
<script src="https://unpkg.com/aos@2.3.1/dist/aos.js"></script>
<script>
  // check if AOS is defined recursively
  function checkAOS() {
    if (typeof AOS !== "undefined") {
      const arr = AOS.init({
        duration: 500,
        duration: 800,
        mirror: false,
        once: true,
      });
      if (!arr) {
        setTimeout(checkAOS, 100);
      }
    } else {
      setTimeout(checkAOS, 100);
    }
  }
  checkAOS();
</script>
<!-- <script src="https://files.easy-orders.net/funnels-assets/souq/assets/js/aos.js"></script> -->
<!-- Initialize Swiper -->
<script src="https://files.easy-orders.net/funnels-assets/souq/assets/js/swiper.js"></script>

<script src="https://unpkg.com/mustache@latest"></script>
<script id="product-data">
  function initMustache() {
    if (!window.Mustache) {
      return setTimeout(initMustache, 50);
    }
    //begin-slides
    const slides = [
      {
        url: "https://files.easy-orders.net/placeholder.webp",
        index: 0,
        isActive: true,
      },
      {
        url: "https://files.easy-orders.net/placeholder.webp",
        index: 1,
        isActive: false,
      },
      {
        url: "https://files.easy-orders.net/placeholder.webp",
        index: 2,
        isActive: false,
      },
      {
        url: "https://files.easy-orders.net/placeholder.webp",
        index: 3,
        isActive: false,
      },
      {
        url: "https://files.easy-orders.net/placeholder.webp",
        index: 4,
        isActive: false,
      },
    ];
    //end-slides

    const template = document.getElementById("gallery-template").innerHTML;
    const rendered = Mustache.render(template, {
      name: "Luke",
      slides,
      isFirst: function () {
        return this.index === 0;
      },
    });
    document.getElementById("carouselExampleIndicators").innerHTML = rendered;
  }
  initMustache();
</script>
```

## summary

:::warning
The total size of the html file or any other file should not exceed **80kb**
:::

:::warning
Don't add internal css or js. instead, use external files you can go to [**Upload assets**](https://seller.easy-orders.net/#/upload-assets) to upload your css and js files and then put the link in the head tag
:::

### The base html template that you can start with

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <meta content="width=device-width, initial-scale=1.0" name="viewport" />

    <title>your product name</title>
    <meta content="" name="description" />
    <meta content="" name="keywords" />

    <!-- Vendor CSS Files -->
    <link
      href="https://files.easy-orders.net/funnels-assets/souq/assets/vendor/bootstrap/css/bootstrap.min.css"
      rel="stylesheet"
    />
    <link
      href="https://files.easy-orders.net/funnels-assets/souq/assets/vendor/swiper/swiper-bundle.min.css"
      rel="stylesheet"
    />
    <!-- fade-up animation [aos] -->
    <link href="https://unpkg.com/aos@2.3.1/dist/aos.css" rel="stylesheet" />

    <!-- Template Main CSS File -->
    <!-- add your external css link here -->
  </head>

  <body>
    <header>
      <h1>Welcome to Our Product</h1>
    </header>

    <main>
      <!-- demo content -->
      <section>
        <h2>Features</h2>
        <article>
          <h3>Feature 1</h3>
          <p>Details about feature 1.</p>
        </article>
        <article>
          <h3>Feature 2</h3>
          <p>Details about feature 2.</p>
        </article>
        <article>
          <h3>Feature 3</h3>
          <p>Details about feature 3.</p>
        </article>
      </section>
    </main>
    <footer>
      <p>&copy; 2023 Your store Name. All rights reserved.</p>
    </footer>

    <!-- Vendor JS Files -->
    <script src="https://files.easy-orders.net/funnels-assets/souq/assets/vendor/bootstrap/js/bootstrap.bundle.min.js"></script>
    <script src="https://files.easy-orders.net/funnels-assets/souq/assets/vendor/swiper/swiper-bundle.min.js"></script>
    <!-- jquery -->
    <script
      src="https://code.jquery.com/jquery-3.7.1.js"
      integrity="sha256-eKhayi8LEQwp4NKxN+CfCh+3qOVUtJn3QNZ0TciWLP4="
      crossorigin="anonymous"
    ></script>

    <!-- fade-up animation [aos] -->
    <script src="https://unpkg.com/aos@2.3.1/dist/aos.js"></script>
    <script>
      // check if AOS is defined recursively
      function checkAOS() {
        if (typeof AOS !== "undefined") {
          const arr = AOS.init({
            duration: 500,
            duration: 800,
            mirror: false,
            once: true,
          });
          if (!arr) {
            setTimeout(checkAOS, 100);
          }
        } else {
          setTimeout(checkAOS, 100);
        }
      }
      checkAOS();
    </script>

    <!-- Initialize Swiper -->
    <script src="https://files.easy-orders.net/funnels-assets/souq/assets/js/swiper.js"></script>

    <script src="https://unpkg.com/mustache@latest"></script>
    <script id="product-data">
      function initMustache() {
        if (!window.Mustache) {
          return setTimeout(initMustache, 50);
        }
        //begin-slides
        const slides = [
          {
            url: "https://files.easy-orders.net/placeholder.webp",
            index: 0,
            isActive: true,
          },
          {
            url: "https://files.easy-orders.net/placeholder.webp",
            index: 1,
            isActive: false,
          },
          {
            url: "https://files.easy-orders.net/placeholder.webp",
            index: 2,
            isActive: false,
          },
          {
            url: "https://files.easy-orders.net/placeholder.webp",
            index: 3,
            isActive: false,
          },
          {
            url: "https://files.easy-orders.net/placeholder.webp",
            index: 4,
            isActive: false,
          },
        ];
        //end-slides

        const template = document.getElementById("gallery-template").innerHTML;
        const rendered = Mustache.render(template, {
          name: "Luke",
          slides,
          isFirst: function () {
            return this.index === 0;
          },
        });
        document.getElementById("carouselExampleIndicators").innerHTML =
          rendered;
      }
      initMustache();
    </script>
  </body>
</html>
```
