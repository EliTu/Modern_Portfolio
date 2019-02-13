# Building a Modern Portfolio Website - By Traversy Media

## Introduction

In this project we will be building a responsive portfolio website from the ground up. We will be using HTML5, CSS3, SASS and a little bit of JavaScript.

### Overview of the finished webpage

- The homepage is very minimalistic. Contains the name, slogan and some social media icons.

- What's special about the website is the menu, that is located in the top right corner of the webpage. The menu opens and closes with CSS transition effects, when the left side rolls from the bottom and the right side rolls from the top. The overlay consists of two section: the left side has an image of the person, and the right side has a nav bar that navigates through different sections of the webpage: Home, About Me, My Work, Contact Info.

- The 'About Me' page is done with CSS Grid and is fully responsive.

- The 'My Work' page also done with CSS Grid and is fully responsive.

- The 'Contact Info' page is done with CSS Flexbox and use CSS transitions for hover effects on the items.

- The website is fully responsive, and the layout changes for smaller screen devices. The main page becomes centered and stacked, The menu transition effects become vertical rather than horizontal fashion. Going through the different pages everything gets stacked responsive. In 'My Work' page the items gets stacked 1 item per row, but as the dimensions grow they become two in a row, later three in a row and in max dimensions the items are sorted 4 in a row.

### Files structure

- We have Node SASS running in the terminal for compiling SASS. All of the SASS we create goes to a SASS folder that hosts the SASS files with the configurations that will be applied to the CSS.

- The SASS code will have various configurations that will be applied to the CSS, for example displaying the background image (or not), Color schemes for the website, background opacity, SASS Mix function that sets the text color based on the background color and more.

- In a separate folder we have all the files we will deploy in the website - the HTML files, main CSS with the compiled SASS and JavaScript files.

- Lastly we have .JSON files.

### Step one: Setting our workflow

We will be using VSC, NPM, and Git throughout this project.

We will then create a new folder called "dist", which inside we will put all the files to be deployed in the server - HTML files,the compiled CSS file(Will be created by itself after initializing SASS), JS files, images etc.

To view the changes in our webpage we will be using live-server extension which will be updating the changes we do with HTML and CSS live automatically.

Next we will create another folder called "scss" which will act as our SASS files folder. We will create a file called "main.scss", which will act as our main SASS file, and any other SASS file we will create will act as partials of that file, that we basically import to that main file.

The browser by itself cannot read SASS files, and so we will need to install node-sass in order for the SASS files to be compiled into regular CSS.

But before we even install node-sass we need to create a package.json file. We can do it through the terminal (integrated VSC terminal or regular OS Bash) typing `npm init`, afterwards we will fill in the relevant information for the .json file and it will create the package.json file, with regular key-value pairs. It holds data and information, and if we will install anything with NPM it will log it inside the 'dependencies' object.

After installing node-sass we can see that a "Node Modules" folder has been created inside our main folder. Anytime we install something with NPM it is being put inside the "Node Modules" folder. If we open the folder we can see many files, and thats because the node-sass has dependencies, and its dependencies also have their own dependencies, but we can ignore these files, we won't need to touch them or the folders inside "Node Modules".

Next we will need to setup the node-sass so it will work. We will go to our package.json file and use an 'npm-script' to initialize it, under the "scripts" object. We will change the default "test" key to "sass" (although we can give it any name we wish), and in the value, between the double-quotes, we will type `"node-sass -w scss/ -o dist/css/ --recursive"`. the `-w` flag means "watch", meaning it will the scss folder and the SASS files inside of it. `-o` flag means "output" and it will output the result into the dist/css folder. lastly, `--recursive` flag is important because it prevents issues with impartials. After we done we will type in the terminal `npm run sass`, and it will start watching the scss folder.

We will test its functionality by going to the "main.scss" file and type some SASS code. We will create a variable for the main color typing `$primary-color: #444`, which is a dark grey color. We will then assign in to the background color of the body tag `body{background: $primary-color}`, and then when we save we get a response back from the console that ran the sass, saying in a green message that the render was successful. Now if we will look in our "dist" folder we can see that we have a new "css" folder with a "main.css" file inside of it, if we open that file we can see that the SASS compiled the code we wrote into normal CSS file upon the save, it displays a normal body tag with the color of grey `body{background: #444}`. We not going to touch the compiled CSS file, but only work with the SASS file. To enable the SASS code in our HTML, we will link the compiles CSS file, "main.css", output in the link tag.

Next we would like to create a new Git repo, but before that we will create a new file called ".gitignore", which will create a new git file inside our folder, and inside this file we will simply write "node_modules", which will ignore the node modules and they will not be added to our repo. Afterwards we will use the terminal to initialize a new git repo, afterwards we can commit the changes as "initial setup", but we do not need to push anything into the master branch as of yet.

## Building the Homepage and Main SASS

### Header part

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
  background-color: $primary-color;
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
    background: rgba(lighten($primary-color, 2), 0.5);
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

We will set the color of the secondary-class we set to the last name at the `<h1>` tag. For that we will set another variable named `$secondary-color` that takes the value of `#eece1a`. I also personally added an `!important` literal so it won't be overridden by another color value in the future.

```scss
$secondary-color: #eece1a;

.text-secondary {
  color: $secondary-color !important;
}
```

### The Main area

This area is everything that is not in the header, meaning the the containers for `<h1>` and `<h2>` and the icons. For the container itself we will add padding and height of 100%. Inside we will also want to style the icons using the SASS nesting, we just refer to the icons container inside the `main` selector using the `.icons` class selector. We will give the container padding, and then we will select the `a` tags to target each link, we will add padding. Next we will want to give the icons color upon hover, and so we will use more nesting to reference the pseudo-class, using the `&` literal and adding `:hover` to it (equivalent to `a:hover` in regular CSS syntax).

Upon hover the color will change to the `$secondary-color` variable, but we will also set a transition effect for making it cooler, and for that we will use a special SASS feature called **Mixin**, which is basically a custom function, because we will be using the same transition effect in many places throughout the project, and so we would like to set a reuseable piece of code. The syntax of declaring a mixin is `@mixin 'functionName'` (a little similar to a function declaration in JavaScript, also needs to be camelCased), and then in the code block include the code. We will call our mixin `@mixin easeOut` To call the mixin function, inside a selector we simply type `@include 'mixin name'`, so it will be `@include easeOut();`, and now upon hovering on the icons we get the color transition effect. Now every time we would like to add this transition effect we should simply call the mixin, and that's exactly what the mixins and variables are made for.

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
        color: $secondary-color;
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

We will start by creating 3 variables. First is `$show-home-image` and its a boolean with a value of `true`. The second variable is the actual image variable `$home-image` with the value of a url that links to the background image in the images folder in our project folder. The third variable will be the `$background-opacity` and it will be set to anywhere between 0.7 and 0.9;

```scss
$show-home-image: true; // display the background image on the homepage
$home-image: url(/dist/img/background.jpg);
$background-opacity: 0.7;
```

### The overlay

At this point, we don't want just the image to be on the site as it will render the text unreadable, we need an overlay element that will make the background darker. We will start by creating another mixin named 'background' for the background overlay, that mixin will be included in the body selector. We would need to make sure if the image is actually being presented in the file and so we will write an `if` statement inside the mixin, the syntax is `@if`, and so we will use our `$show-home-image` that we've created earlier, so `@if $show-home-image` (boolean, by default value = true), them we will present the background image and create the overlay over the `<body>` tag by using the `bg-img` id we gave it.

We will select the `<body>` tag id using the `&` literal and set the background image, and set its size to cover the whole page. Now without the overlay the image is too bright and makes some of the text unreadable, and so we will create an overlay using the `:after` pseudo-element, which basically allows the CSS to treat it as an element in the HTML page without it actually being one, and so we again select it using the `&` literal, giving it a blank `content` property, top and right value of 0, position absolute, width and height of 100% (so it will stretch over the entire page) and give it color values of our variables `$primary-color` and `$primary-opacity` as rgba function arguments. At this point, We get the right coloring and sizing of the overlay, but the problem is that the page content is behind the overlay, as it is an "after" element that by default sits on top of the content, and so we will give it a negative `z-index` in order to make it secondary, or behind, the page content.

```scss
@mixin background {
  @if $show-home-image {
    &#bg-img {
      background: $home-image;
      background-attachment: fixed;
      background-size: cover;

      &:after {
        content: "";
        position: absolute;
        top: 0;
        right: 0;
        width: 100%;
        height: 100%;
        background: rgba($primary-color, $background-opacity);
        z-index: -1;
      }
    }
  }
}
```

### Creating the '\_config' SASS partial file

At this point all of our SASS variables and mixins are getting numerous, and they will only get larger as the project goes, so at we would like to create a new SASS file that will act as our **partial**, meaning a component of the SASS files, which we could 'merge' with the main SASS file that we've been using so far, and thus making the code cleaner and leaner looking.

We will create a new file in the 'scss' folder and call it '\_config.scss',take all the variables and mixins we've created and put it inside that file. After we do that, the console that the SASS is running and looking at the SASS code will turn red and display errors, stating that part of the code is gone, and so we will **import** that '\_config' file to our main SASS file using the `@import` syntax, with the name of the file (without the underscore). This in turn will make the errors disappear

```scss
@import "config";
```

##
