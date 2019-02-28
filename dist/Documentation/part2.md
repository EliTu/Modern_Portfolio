# Part 2 - Building the Homepage and Main SASS

### The header part

We will start by creating the markup elements of the HTML page, basically everything that is on the landing page of the website. We will start with the `<header>` section of the webpage, that will include the main menu that will include the site navigation links.

We will first create the markup for the custom built menu, all made of `<div>` elements, these will act as the layout of the menu:

```html
<div class="menu-btn">
  <div class="btn-line"></div>
  <div class="btn-line"></div>
  <div class="btn-line"></div>
</div>
```

Next we will create the menu nav page itself. As we saw, the menu will consist of the left side, which will have a portrait, and right side which will have the nav `<a>` links themselves. These two parts will be divided by two different `<div>` elements. The nav menu will consist of a `<ul>` with 3 `<li>` elements with `<a>` nested in them, each leads to a different part of the site.

```html
<nav class="menu">
  <div class="menu-branding">
    <div class="portrait"></div>
  </div>

  <ul class="menu-nav">
    <li class="nav-item">
      <a href="/about.html" class="nav-link">About Me</a>
    </li>
    <li class="nav-item">
      <a href="/work.html" class="nav-link">My Work</a>
    </li>
    <li class="nav-item">
      <a href="/contact.html" class="nav-link">Contact Me</a>
    </li>
  </ul>
</nav>
```

### Main area

Inside the main area we will include our `<h1>` with the class of "lg-heading" (stands for large-heading) and `<h2>` tag with the class of "sm-headings" (stands for small-heading). We will also wrap the last name with a `<span>`so we could customize its colors later.

```html
<h1 class="lg-heading">Eliad <span class="text-secondary"> Touksher</span></h1>
<h2 class="sm-heading">Hi, I am a developer and I solve problems!</h2>
```

We would like to add some social media Icons under the headings, and for that we will use Font Awesome icons, so first we will import the Font Awesome library using the `<link>` tags.

```html
<link
  rel="stylesheet"
  href="https://use.fontawesome.com/releases/v5.7.1/css/all.css"
  integrity="sha384-fnmOCqbTlWIlj8LyTjo7mOUStjsKC4pOpQbqyi7RrhN7udi9RwhKkMHpvLbHG9Sr"
  crossorigin="anonymous"
/>
```

Now we will put a `<div>` with the class of "icons" and in it we will have 4 `<a>` tags, each got a special FA icon using the `<i>` tags, corresponding to the social media platform, and also class of "fa-2x" that will enlarge them (size: 2x).

```html
<div class="icons">
  <a href="#">
    <i class="fab fa-twitter fa-2x" aria-hidden="true"></i>
  </a>
  <a href="#">
    <i class="fab fa-facebook fa-2x" aria-hidden="true"></i>
  </a>
  <a href="#">
    <i class="fab fa-linkedin fa-2x" aria-hidden="true"></i>
  </a>
  <a href="#">
    <i class="fab fa-github fa-2x" aria-hidden="true"></i>
  </a>
</div>
```

### Script tag

Last thing we will add at this point to the markup section of the page is the link to the JavaScript file, using the `<script>` tag
linking to the location of the file in the project folder.

```html
<script src="/dist/JS/script.js"></script>
```

## Styling the home page using SASS (CSS)

### General styling

We will start with editing the box-sizing of the page, and we will be targeting the whole document using the '\*' selector. This will make sure that any padding or background won't affect the width or the height, and so we will have a better box-model.

```scss
* {
  box-sizing: border-box;
}
```

Next we will move to the `body` of the page and set some general styling rules - height and 100%, 0 margins, set a better font etc.

```scss
body {
  background-color: primary-color;
  height: 100%;
  margin: 0;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  line-height: 1.5;
}
```

### Headings

Next we will like to take care of the heading tags in our file, which will include `<h1>`, `<h2>` and `<h3>`. We will cancel the margins, lighten the font-weight and have a color. Next we will do some SASS nesting in order to target the headings with the classes we've set. The syntax for targeting the classes of the selected elements is the `&` prefix following a `.classname`, and then opening a new code scope. If we wanted to select the classes of elements inside the headings, we could simply omit the `&` prefix, that way children elements that are nested in headings will be targeted. We will set the font-size with rem units, set paddings, and give the background of the `<h2>` tag with rgba function that has another special SASS function called `lighten()` that takes 2 colors as arguments, one is the original color, in our case its the `&primary-color` variable, and the second is how much we want to make it lighter, after we set the colors of the rgba function we will implement the last opacity value and give it 0.5.

```scss
h1,
h2,
h3 {
  margin: 0;
  font-weight: 400;
  color: #eef;

  &.lg-heading {
    font-size: 6rem;
  }

  &.sm-heading {
    margin-bottom: 2rem;
    padding: 0.2rem 1rem;
    background: rgba(lighten(primary-color, 2), 0.5);
  }
}
```

### Links

We will set standard settings for the links: give them color and remove the default underline.

```scss
a {
  color: white;
  text-decoration: none;
}
```

### Header area

We will set the position of the header (the menu button) to `fixed`, as we want it to always stay at the top, even if we have to scroll the page. Next we will put a `z-index` of positive 2, so we will make sure it will always stay on top and won't be somehow set behind a different element of layer. The width will be set to 100% so when the menu will open up it will be stretched through the whole screen.

```scss
header {
  position: fixed;
  z-index: 2;
  width: 100%;
}
```

### The secondary-text class

We will set the color of the secondary-class we set to the last name at the `<h1>` tag. For that we will set another variable named `secondary-color` that takes the value of `#eece1a`. I also personally added an `!important` literal so it won't be overridden by another color value in the future.

```scss
secondary-color: #eece1a;

.text-secondary {
  color: secondary-color !important;
}
```

### The Main area

This area is everything that is not in the header, meaning the the containers for `<h1>` and `<h2>` and the icons. For the container itself we will add padding and height of 100%. Inside we will also want to style the icons using the SASS nesting, we just refer to the icons container inside the `main` selector using the `.icons` class selector. We will give the container padding, and then we will select the `a` tags to target each link, we will add padding. Next we will want to give the icons color upon hover, and so we will use more nesting to reference the pseudo-class, using the `&` literal and adding `:hover` to it (equivalent to `a:hover` in regular CSS syntax).

Upon hover the color will change to the `secondary-color` variable, but we will also set a transition effect for making it cooler, and for that we will use a special SASS feature called **Mixin**, which is basically a custom function, because we will be using the same transition effect in many places throughout the project, and so we would like to set a reuseable piece of code. The syntax of declaring a mixin is `@mixin 'functionName'` (a little similar to a function declaration in JavaScript, also needs to be camelCased), and then in the code block include the code. We will call our mixin `@mixin easeOut` To call the mixin function, inside a selector we simply type `@include 'mixin name'`, so it will be `@include easeOut();`, and now upon hovering on the icons we get the color transition effect. Now every time we would like to add this transition effect we should simply call the mixin, and that's exactly what the mixins and variables are made for.

Next we would like to move the whole "main" container box downward,and we can do this easily with the id we gave the `<main>` tag, so we can target that using the `&` literal targeting `#home`. Inisde we will set the `overflow` property to "hidden", as we don't want any scrollables at our home page, and give the h1 a specific margin to move it downwards, using `vh` units (viewport height, out of 100).

```scss
@mixin easeOut {
  transition: all 0.4s ease-out;
}

main {
  padding: 4rem;
  height: 100%;

  .icons {
    margin-top: 1rem;

    a {
      padding: 0.4rem;

      &:hover {
        color: secondary-color;
        @include easeOut(); // Use mixin function.
      }
    }
  }

  &#home {
    overflow: hidden;
    h1 {
      margin-top: 20vh;
    }
  }
}
```

### The background image

We will start by creating 3 variables. First is `show-home-image` and its a boolean with a value of `true`. The second variable is the actual image variable `home-image` with the value of a url that links to the background image in the images folder in our project folder. The third variable will be the `background-opacity` and it will be set to anywhere between 0.7 and 0.9;

```scss
show-home-image: true; // display the background image on the homepage
home-image: url(/dist/img/background.jpg);
background-opacity: 0.7;
```

### The overlay

At this point, we don't want just the image to be on the site as it will render the text unreadable, we need an overlay element that will make the background darker. We will start by creating another mixin named 'background' for the background overlay, that mixin will be included in the body selector. We would need to make sure if the image is actually being presented in the file and so we will write an `if` statement inside the mixin, the syntax is `@if`, and so we will use our `show-home-image` that we've created earlier, so `@if show-home-image` (boolean, by default value = true), them we will present the background image and create the overlay over the `<body>` tag by using the `bg-img` id we gave it.

We will select the `<body>` tag id using the `&` literal and set the background image, and set its size to cover the whole page. Now without the overlay the image is too bright and makes some of the text unreadable, and so we will create an overlay using the `:after` pseudo-element, which basically allows the CSS to treat it as an element in the HTML page without it actually being one, and so we again select it using the `&` literal, giving it a blank `content` property, top and right value of 0, position absolute, width and height of 100% (so it will stretch over the entire page) and give it color values of our variables `primary-color` and `primary-opacity` as rgba function arguments. At this point, We get the right coloring and sizing of the overlay, but the problem is that the page content is behind the overlay, as it is an "after" element that by default sits on top of the content, and so we will give it a negative `z-index` in order to make it secondary, or behind, the page content.

```scss
@mixin background {
  @if show-home-image {
    &#bg-img {
      background: home-image;
      background-attachment: fixed;
      background-size: cover;

      &:after {
        content: "";
        position: absolute;
        top: 0;
        right: 0;
        width: 100%;
        height: 100%;
        background: rgba(primary-color, background-opacity);
        z-index: -1;
      }
    }
  }
}
```
