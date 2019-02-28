## Part 1 - Intro & SASS Workflow setup

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

# Part 2 - Building the Homepage and Main SASS

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

# Part 3 - Rotating Menu Button

### Creating the '\_config' SASS partial file

At this point all of our SASS variables and mixins are getting numerous, and they will only get larger as the project goes, so at we would like to create a new SASS file that will act as our **partial**, meaning a component of the SASS files, which we could 'merge' with the main SASS file that we've been using so far, and thus making the code cleaner and leaner looking.

We will create a new file in the 'scss' folder and call it '\_config.scss',take all the variables and mixins we've created and put it inside that file. After we do that, the console that the SASS is running and looking at the SASS code will turn red and display errors, stating that part of the code is gone, and so we will **import** that '\_config' file to our main SASS file using the `@import` syntax, with the name of the file (without the underscore). This in turn will make the errors disappear

```scss
@import "config";
```

## Creating the menu button

### Menu button SASS design

For the menu, we will have a separate scss file, since it will involve quite a bit of SASS design, and so to keep the code clean we will separate between the 'main' file and create '\_menu.scss' file, and as we did with the config file, we will use `@import` on the main file to add it to our 'main' scss file.

## Menu button container

We want to build out our menu button, using pure CSS on the HTML elements designated for the 'menu' button.

```html
<div class="menu-btn">
  <div class="btn-line"></div>
  <div class="btn-line"></div>
  <div class="btn-line"></div>
</div>
```

So first we will work on the `menu-btn` class container. We want it at `position: absolute` and in the top right corner of the page, also we want it always to be on top, and so we will also indicate a high `z-index`. Another thing that we will add is our 'transition' mixin function, so it will also have the nice transition effect.

```scss
.menu-btn {
  position: absolute;
  z-index: 3;
  right: 35px;
  top: 35px;
  cursor: pointer;
  @include easeOut();
}
```

## Menu button layout

Next we will want to create the general layout of the button, which are the three lines that will act as the clickable graphical feature, which are represented by the 3 `<div>` tags with the class of 'btn-line'. We will give them a width and height, and that will make them visible on the page. We will also apply the `easeOut` mixin on here as well, as we want to have a transition effect not only on the button container but also on the item 'lines' as well. After saving, we should be able to see the 3 white lines at the top right corner of the screen.

```scss
.menu-btn {
  position: absolute;
  z-index: 3;
  right: 35px;
  top: 35px;
  cursor: pointer;
  @include easeOut();

  .btn-line {
    width: 28px;
    height: 3px;
    margin: 0 0 5px 0;
    background: #fff;
    @include easeOut();
  }
}
```

## Configuring the JavaScript

At this point we can go ahead and start adding the JavaScript for the page, which will basically will be used to create an event listener in order to listen to a 'click' event on the button, and then apply new classes for the various menu-button elements. We will write the JavaScript code inside the main JavaScript file named 'script.js' file in the 'JS' folder.

## Selecting DOM items

We want to select the DOM elements that correspond with the menu and the menu items UI. And so we will get all these HTML elements using the `querySelector` method, and store them in a variable. The 'nav-items', which represents the clickable links, we will use the `querySelectorALl` method, as the items are numerous, and this will give us a node list that we can loop over later to target each specific item that corresponds to 'nav-item' class element.

```js
const menuBtn = document.querySelector(".menu-btn");
const menu = document.querySelector(".menu");
const menuNav = document.querySelector(".menu-nav");
const menuBranding = document.querySelector(".menu-branding");
const navItems = document.querySelectorAll(".nav-item");
```

## Setting the menu state variable

After we've selected all the relevant DOM items we want to set the 'initial state' of the menu, meaning the overlay design option. We will create a variable that will represent if the menu is at an 'open' or 'closed' state, which will be represented by a boolean (true === open, false === closed). By default we would like it to be closed. This time the variable will be declared with a `let`, as we want it to be mutable to change between `true` and `false`.

```js
let showMenu = false;
```

## Creating the event listener and the function

We want to create an event listener that will listen to a click event on the button, and once the button got clicked we want a function to be fired that will change the state variable `showMenu` and will make more changes in the DOM elements of the menu.

```js
menuBtn.addEventListener("click", toggleMenu);
```

Next we would want to create the `toggleMenu` function that will be called upon a click on the menu button. First thing we will need to do is create an `if/else` statement that will check the current state of the menu (if it's open or closed at the time of the click). If the state is `!showMenu` (`showMenu === false`) so we will want to add the 'show' classes to the menu items, since we want them to become visible, and 'close' class for the menu button since we want it to be available for closing ('X' shape that we will design later). We will use the `classList.add()` method to add the relevant classes. For the `navItems` variable, which holds the nav items, we will need to loop through all of the items, so we will use `forEach()` method to loop over all the items to select them all, and then we will apply the `classList.add()` method for them as well to add the 'show' class. At the end we want to 'reset' the menu state, so if the menu was closed, so the value of the variable was `false`, we want to change the value to `true`, to set the menu for an open state and make the 'close' options available.

```js
function toggleMenu() {
  if (!showMenu) {
    menuBtn.classList.add("close");
    menu.classList.add("show");
    menuNav.classList.add("show");
    menuBranding.classList.add("show");
    navItems.forEach(item => item.classList.add("show"));

    // Set menu state
    showMenu = true;
  } else {
  }
}
```

In the `else` block, we will do the exact same thing as we did in the `if` statement code block, only we will remove the classes we added and set the value of `showMenu` to `false`. And with that, it should be all the JavaScript we need at this point. We can look at the developer tools 'elements' tab, look at the relevant menu elements and see if upon a click the classes are being added and removed as intended.

```js
function toggleMenu() {
  if (!showMenu) {
    menuBtn.classList.add("close");
    menu.classList.add("show");
    menuNav.classList.add("show");
    menuBranding.classList.add("show");
    navItems.forEach(item => item.classList.add("show"));

    // Set menu state
    showMenu = true;
  } else {
    menuBtn.classList.remove("close");
    menu.classList.remove("show");
    menuNav.classList.remove("show");
    menuBranding.classList.remove("show");
    navItems.forEach(item => item.classList.remove("show"));

    // Set menu state
    showMenu = false;
  }
}
```

## Adding the "close" class and adding the rotate to 'X' transition

We will return to the SASS menu file and continue to work on the styles, now that we got the JavaScript working. WE will use the `&` literal to select the 'close' class that is added to the `menu-btn` element upon a click, and add the transition into an 'X' shape from the 3 dash lines look to symbolize the closing option. We would want to make a CSS transition for that, and so it will make a small animation of a rotation and then transform to the 'X'.

```scss
&.close {
    transform: rotate(180deg);
}
```

Now at this point, upon a click on the menu button it will perform a 180 degree rotation animation, which is one part of the desired effect we want, but now we need the transformation animation of each line, basically we want to form an 'X' symbol, and so we need to reposition the top and bottom lines, and make the middle one disappear. For this, we want to select each line separately (as each is represented by a `<div>` element), and so we will first select the lines with the selector `.btn-line`, and to represent each line we will use a pseudo-selector `:nth-child()` to select each one by order of position in the HTML page.

```scss
&.close {
  transform: rotate(180deg);

  .btn-line {
    // Line 1 - rotate:
    &:nth-child(1) {
    }

    // Line 2 - hide:
    &:nth-child(2) {
    }

    // Line 3 - rotate:
    &:nth-child(3) {
    }
  }
}
```

Now we would like to add the animations to each line desperately. In order for us to be able to make the transition from a straight line to a diagonal line, we will need to use `rotate()` and then `translate()` animations to reposition the lines. The middle line (`&:nth-child(2)`) we will simply set its `opacity` to 0 in order to make him disappear/reappear upon the click.

```scss
&.close {
  transform: rotate(180deg);

  .btn-line {
    // Line 1 - rotate:
    &:nth-child(1) {
      transform-origin: center;
      transform: rotate(45deg) translate(5px, 5px);
    }

    // Line 2 - hide:
    &:nth-child(2) {
      opacity: 0;
    }

    // Line 3 - rotate:
    &:nth-child(3) {
      transform-origin: center;
      transform: rotate(-45deg) translate(7px, -6px);
    }
  }
}
```

# Part 4 - Creating the menu and overlay & Responsive Media Queries

### Setting the menu overlay

To work on the overlay, we will first want to set the the overlay design and the general wrapper of the menu, editing the `.menu` class element. We would want to give it a `fixed` position, as we don't want it to be scrollable, we will give it a `width` of 100% as we want it to cover the whole screen. We will give it `opacity` of 0.96 as we want it to be a bit see through. We want to set its state `visibility`, and so by default, meaning up until we press the menu button, we want it to be `hidden`, only after we add the class of `.show`, which is done by pressing on the menu button, the `visibility` will be changed to `visible`.

```scss
.menu {
    position: fixed;
    top: 0;
    width: 100%;
    opacity: 0.96;
    visibility: hidden; // By default. Visible only upon a click.

    &.show {
        visibility: visible;
    }
}
```

### Setting the menu content - portrait and Nav items

Now that we set the initial overlay outer design and state, we will now fill it with the content of the menu, which will be the nav bar items who would be placed on the right and the portrait who will be placed on the left. We will start with the containers of the portrait and the nav items box. To select the portrait, which is represented by the `<div>` with the class of `menu-branding`, and so to select it in SASS, we can simply use the `&` literal inside the `.menu` selector and pass `-branding` and it will represent `menu-branding`. Similarly, we will select the `menu-nav`.

We want to apply flexbox display to them with a division for two columns, by default each take 50% of the screen. We will use `align-items` to the center and `justify-content` to the center, so the items will be aligned both vertically and horizontally to the center. They both will have `float` value of `left`, and `width` of 50% each. For the `height`, since we want it to be the whole screen, we will set it to `100vh`, which can be represented as 100vh = 100% of the screen. Lastly, we will set the overflow to hidden, as we don't want any scroll bars.

```scss
// Set the display of both overlay sides
&-branding,
&-nav {
  display: flex;
  flex-flow: column wrap;
  align-items: center;
  justify-content: center;
  float: left;
  width: 50%;
  height: 100vh;
  overflow: hidden;
}
```

### Styling each side of the menu individually - The nav side

We will start with the right side, which is the nav menu. We will 0 the `margin` and the `padding`. We will set a background color to a darker version of the `$primary-color` variable using the SASS `darken()` function (later I set it all inside an `rgba()` function to give it an opacity value).

Next we would like to style the opening transition effect ,as we want it to slide from the top, and so we will use `transform: translate3d()` values to achieve that effect. the `translate3d()` takes positioning parameters and moves in the selected item inside the container (also can be outside the container, as in our case), we will give an initial value of `(0, -100%, 0)` which will offset the nav-items box outside the page on the top side by default, and then when we will click on the menu button and the `.show` class will be applied, we will restore the values to the default `(0, 0, 0)` and then it will position the nav item box in its set position. We will also include our mixin of `easeOut()` to make the transition smooth.

```scss
&-nav {
  margin: 0;
  padding: 0;
  background: rgba(darken($primary-color, 5), 0.9);
  list-style: none;
  transform: translate3d(
    0,
    -100%,
    0
  ); // Initial position, off the screen at the top
  @include easeOut();

  &.show {
    // Slide in from the top
    transform: translate3d(0, 0, 0); // Transition initial position
  }
}
```

### Styling each side of the menu individually - The branding side

Now we would like to similarly style the branding side box, which will also include the portrait itself inside of it. We will target the `menu-branding` individually like we did with `&-nav`, and now we will apply individual styles to that box.

We set the `background` as the `$primary-color` (and I give it rgba() function for the opacity), include the mixin for the smooth transition and do the same thing with the `transform: translate3d()`, only this time we want this side of the menu to slide from the bottom, and so we set the Y-value at the opposite side of the nav side, and so the values will be set to `(0, 100%, 0)`, and by default the left side of the menu will be offset outside the viewport at the bottom, and only upon applying the `.show` class it will slide in from the bottom to its default position.

Next we would like to add in the portrait so the left side will have content. The portrait is an HTML `<div>`, and so we will select its class and give it an `background` with a `url()` of the image in our 'img' folder, next we will set its `width` and `height` to be smaller and give it a round cover using `border-radius` value of 50% and a solid `border`. Lastly, we will set `opacity` value of 1 in order for the image not to be transparent.

```scss
&-branding {
  background: rgba($primary-color, 0.9);
  @include easeOut();
  transform: translate3d(
    0,
    100%,
    0
  ); // Initial position, of the screen at the bottom

  &.show {
    // Slide in from the bottom
    transform: translate3d(0, 0, 0); // Transition initial position
  }

  .portrait {
    width: 250px;
    height: 250px;
    background: url("/dist/img/portrait.jpg");
    border-radius: 50%;
    border: solid 3px $secondary-color;
    opacity: 1;
  }
}
```

### Styling the nav items

We want to set the nav items each off the screen as well, as eventually we want them to be transitioned into the screen with the container, after pressing on the menu button. So we will again set `transform: translate3d()` to achieve the desired effect, only this time we're on the X-axis, and so we would want to offset the nav-items off the screen to the right, and so we will give it a value of `(600, 0, 0)`. As usual we will include the `easeOut()` for the smooth-transition, and when the `.show` class is applied, we want to set it back to the default position. Lastly we set a special new class named `current` which will permanently 'mark' the current page (represented by the `<a>` tag) we're on with the `$secondary-color`, by default its the home page.

```scss
.nav-item {
  transform: translate3d(
    600px,
    0,
    0
  ); // Initial position, off the screen to the right
  @include easeOut();

  &.show {
    // Slide in from the right
    transform: translate3d(0, 0, 0); // Transition initial position
  }

  &.current > a {
    color: $secondary-color;
  }
}
```

At this point the menu items are sliding in from the right, but the problem is that all of the items are sliding in at once, and it doesn't look as good as it can be, so we would like to give it the rule so that every item can slide in individually and with a small delay on each variable (that is being looped 4 times) and give it a 0.05 seconds delay. Like that, the nav items will come one by one with a small delay, and not all at once.

```scss
// Delay each nav item slide by 0.1 seconds - SASS for loop
@for $x from 1 through 4 {
  .nav-item:nth-child(#{$x}) {
    transition-delay: $x * 0.05s;
  }
}
```

### Styling the links

Now we want to style the links of the nav items individually. We will display them as `inline-block` with a `relative` position, and also after the style options we will include the mixin. Upon a hover we will apply the `$secondary-color`.

```scss
.nav-link {
  display: inline-block;
  position: relative;
  font-size: 30px;
  text-transform: uppercase;
  padding: 1rem 0;
  font-weight: 300;
  color: #fff;
  text-decoration: none;
  @include easeOut();

  &:hover {
    color: $secondary-color;
  }
}
```

## Setting the initial mobile-responsive features with media queries

### Initializing the media queries

In SASS, the media queries are done with mixins, and so we will set them in the 'config' file. We would like to design our website to be available in 4 different modes, or sizes: Small for smartphones(max-width: 500px), Medium for tablets and small laptops(max-width: 768px), Large for laptops and desktops(min-width: 769px, max-width: 1170px), and Extra large for wide-screens(min-width: 1171px). At the 'config' file we will set a mixin function for each mode, with the specific pixel variation according to the screen sizes. Since this is a mixin, we do not have to specify the code block immediately, as this is the 'config' file, and so we would use the `@content` which will import specs from a different place, or file, where the mixin will be located.

```scss
@mixin mediaSm {
  // Small devices
  @media screen and (max-width: 500px) {
    @content;
  }
}

@mixin mediaMd {
  // Medium devices
  @media screen and (max-width: 768px) {
    @content;
  }
}

@mixin mediaLg {
  // Large devices, has a range
  @media screen and (min-width: 769px) and (max-width: 1170px) {
    @content;
  }
}

@mixin mediaXl {
  // Extra large
  @media screen and (min-width: 1171px) {
    @content;
  }
}
```

### Styling the media queries

For filling the specs of the media queries with styles, we will create a separate file called `_mobile.scss`, and before anything we will go to the 'main' file and use `@import` to link the partial to the main scss file. Inside the 'mobile' file we will use `@include` to get the mixins, we will start from the mixin with the largest media-query specs to the lowest. Everything we will pass in the code block will be the actual specifications of the media queries to be applied in the website.

```scss
// Extra large devices (Wide screens)
@include mediaXl {
}

// Large devices (Desktops & laptops)
@include mediaLg {
}

// Medium devices (Tablets and small laptops)
@include mediaMd {
}

// Small devices (Smartphones)
@include mediaSm {
}
```

### Styling the medium size media query

We will start with the `mediaMd` media query. Before we do the overlay, we will first want to specify the position and size of the main page. We will just use the `<main>` tag as a selector and start repositioning and realigning items, as well as resizing the headings.

```scss
@include mediaMd {
  main {
    align-items: center;
    text-align: center;

    .lg-heading {
      line-height: 1;
      margin-bottom: 1rem;
    }
  }
}
```

Next we will start styling the menu inside the `mediaMd` media query. We will mark `ul.menu-nav` and `div.menu-branding` to select the specific elements we need to configure. We would cancel the `float`, and so we will set it to `none`, this way both part of the menu will not be floating side by side, and so we will also set the `width` to 100% and not 50% for each part of the menu.

```scss
ul.menu-nav,
div.menu-branding {
  float: none;
  width: 100%;
  min-height: 0;

  &.show {
    transform: translate3d(0, 0, 0);
  }
}
```

Next we would like to change the transition of the menu parts, we don't want them to slide from the bottom and the top (y-axis, the 2nd parameter), but from the left and right (x-axis, the 1st parameter), and so we will also reset the `transform: translate3d()` values. I've also included the the `nav-item` in the change of the transition slide location, and now they come from the left and not the right. We will also change the position of the items and the space their taking the medium sized page, as now they are both located on the same column, and so we will give the `.menu-branding` a value of `25vh` (25% of the viewport) and for the `menu-nav` we set `75vh`(75% of the viewport). Next we will set a smaller size image for the portrait (from the 'img' folder), and scale it down as well.

```scss
menu-nav {
  height: 75vh;
  transform: translate3d(-100%, 0, 0);
  font-size: 1.5rem;

  .nav-item {
    transform: translate3d(-600%, 0, 0);
  }
}

.menu-branding {
  height: 25vh;
  transform: translate3d(100%, 0, 0);

  .portrait {
    background: url(/dist/img/portrait_small.jpg);
    width: 150px;
    height: 150px;
  }
}
```

### Styling the small size media query

For the small size media query, we would like to set the `<h1>` of the home page to a `margin-top: 10vh`, meaning that no matter how small or low the phone goes, the heading will stay in a top position.

```scss
@include mediaSm {
  body {
    padding: 0;
    margin: 0 auto;
  }

  main #home h1 {
    margin-top: 10vh;
    font-size: 1rem;
  }

  .lg-heading {
    font-size: 3rem;
  }
}
```

# Part 5 - Creating the 'About' page, styling with CSS Grid and implementing SASS function

### Creating a flexible text color setting using SASS functions

Basically if we want in the future to set the background color to a lighter color, it will render the text color unreadable, since the text color is set to white, and we will have to manually change all the CSS settings of the color property. So in order to make our lives easier we will set a SASS function that will allow us to change the text color, according to the color of the background.

**This has to be a function, and not a mixin** as we expect it to `return` a color value, and you cannot `return` values using mixins. The syntax of a SASS function is similar to a function in JavaScript, only we add '@' at the beginning of the declaration keywords and an '\$' at the beginning of variables. In order for the function to work as we intend we will also add an 'if' statement to check the lightness of the color we pass in the argument, if it's light enough the color we will return will be black, if not then it'll be white.

```scss
@function set-text-color($color) {
  @if (lightness($color) > 40) {
    @return #000;
  } @else {
    @return #fff;
  }
}
```

To call this function, we will go back to the 'main' SASS file and in the `body` selector, we will change the `color` property from `#fff` to the name of the function and pass in the `$primary-color` as an argument. Since the `$primary-color` variable is set to a dark color, the text color that will be returned will be a white color. If we will change the rgba values of the `#primary-color` variable to a light color, the text in the body of the page will be black. We will do the same for the `background` property of the `btn-line` selector (as for the button lines we use background colors and not text colors) and for the `color` of the `nav-link`.

```scss
body {
  ...color: set-text-color($primary-color);
}
```

### Creating the 'About' HTML page

First we will create a new about.html file in the dist folder and link it from the 'Home' page html in the `nav-links`, as well as change the 'current' class to the 'about' nav link. Basically in a new page we would want to keep most of the components we already included in the 'Home' page, such as the menu and its functionality, and only change the content of the page itself, so it'll be safe to just copy-paste the index.html into about.html and simply remove the content area.

- At this point I won't write in detail about every addition of content we make in the 'About' HTML page as it's pretty straightforward, we're just adding a typical bio content. For more reference, simply refer to the 'About' HTML page to look at the elements and the markup structure.
- However, it is worth to mention that at this point we do add a `<footer>` to the HTML page, as we want to have a footer set for the other content pages.

After we finished with the HTML, we would like to remove the background image that was set for the 'Home' page, so we will only have a dark-grey background color. We can do that by simply removing the `bg-img` id we set for the `<body>` tag in the 'Home' page, and thus we negate the effect of the background image mixin that sets the image.

### Aligning the page elements using CSS Grid

We will now align the items in the page by using the grid rules with `grid-template-areas` to map out the location of the items across the grid (the container). First, we would like to set the grid area container, which will be the `<div>` that is containing the content elements (not the headers), with the class of 'about-info'.

```scss
.about-info {
  display: grid;
}
```

Now we can add the `grid-template-areas`, which is a visual mapping of the way we will implement the positioning and scale of the items on the grid, done by placing items as rows and columns between two ' '. For each item, or 'area', we will give it a name that later will correspond to an actual element in the page. If we repeat the name multiple times in the row or column, it will mean that the area that the same item is stretching on will be bigger. In our case, we set the first row as `bio-image bio bio`, which sets the image to take one fraction of the row, while the textual part will take 2 fractions of that row. The second row will be set with 3 equal fractions of `job-1 job-2 job-3`.

```scss
.about-info {
  display: grid;
  grid-template-areas:
    "bio-image bio bio"
    "job-1 job-2 job-3";
}
```

The next thing we will take care of is the `grid-template-columns`, and we want to set it for 3 fractions. We can do it by setting the value to `1fr 1fr 1fr`, but we can do it in a more clean way by using a `repeat()` method and setting the value to `repeat(3, fr)`, which will repeat the fraction 3 times.

```scss
.about-info {
  display: grid;
  grid-template-areas:
    "bio-image bio bio"
    "job-1 job-2 job-3";
  grid-template-columns: repeat(3, 1fr);
}
```

At this point, the container does display as a grid but the elements are not placed as we wanted, and that's because we haven't defined the grid areas with our actual elements. We will now add every individual element that is needed to be placed on the grid, and assign to him the corresponding `grid-template-areas` position. This in turn will set the grid items in the desired positions: the image take one fraction, the bio takes 2 fractions and each 'job' element takes one fraction each.

```scss
.bio-image {
  grid-area: bio-image;
}

.bio {
  grid-area: bio;
}

.job-1 {
  grid-area: job-1;
}

.job-2 {
  grid-area: job-2;
}

.job-3 {
  grid-area: job-3;
}
```

Now we can style the items themselves to look good and professional.

```scss
.bio-image {
  grid-area: bio-image;
  margin: auto;
  border-radius: 50%;
  border: $secondary-color 3px solid;
}

.bio {
  grid-area: bio;
  font-size: 1.5rem;
}

.job-1 {
  grid-area: job-1;
}

.job-2 {
  grid-area: job-2;
}

.job-3 {
  grid-area: job-3;
}

.job {
  background: lighten($primary-color, 5);
  padding: 0.5rem;
  border-bottom: $secondary-color 5px solid;
  text-align: center;
}
```

### Styling the footer

We will first style the footer to look and feel better, by setting `background`, `color`, `height`, `text-align: center` etc.

```scss
#main-footer {
  text-align: center;
  padding: 1rem;
  background: darken($primary-color, 10);
  color: set-text-color($primary-color);
  height: 60px;
}
```

The main issue we will have to deal with the footer is its default position - it is not automatically stuck at the bottom of the page, and if the content will move or we will have a page with less content in the middle, the footer will move itself upwards, and so we would like to prevent it by making a "sticky footer". We can do that by going to the parent element of the footer, which in our case is the `<main>` tag, and use a `calc()` function in the `height` property to set its position permanently. Right now, the `main` selector has a `height` of 100%, which basically sets the height to 100% of the content that's inside of it, so if the content ends closer to the top of the page, the footer will also move up. So instead of using `height: 100%`, we will use `min-height` and use the value to calculate the full viewport height and take off the `height` of the footer, which is 60px, and so we wil lget `min-height: calc(100vh-60px);`. Now the footer will stick at the bottom as we made sure the height will accord to the viewport height.

```scss
main {
    // height: 100%;
    min-height: calc(100vh - 60px);
}
```

### Making the 'About' page responsive - adding to the 'mobile' partial file

Now we would like our 'About' page to look good on medium screens anw below, and so we will add rules to the media queries in the 'mobile' SASS partial file. The main objective is to change the orientation of the `grid-template-areas`, by making the items stack upon each other instead of being spread out. And so, inside the 'medium' device media query, we will change the position of the `grid-template-areas` of the items inside the grid container. Next, correspondingly, we will also change the `grid-template-columns` into a single column.

```scss
@include mediaMd {
  .about-info {
    grid-template-areas:
      "bio-image"
      "bio"
      "job-1"
      "job-2"
      "job-3";
    grid-template-columns: 1fr;
  }
}
```

# Part 6 - Adding the 'My Work' page & 'Contact' page, and more styling with CSS Grid and Flexbox

### Forming the 'My Work' page markup

Like we've done before, we will go to the 'dist' folder and create a a new html file named 'work.html', which will be serve as markup page for presenting personal projects on the portfolio site. Like we've done before, we'll just base the markup on the 'About Me' page, we'll just change the headings, move the 'current' class and change the whole content of the page.

For presenting the projects, we will have several boxes that each will represent a project, each box will include an image (from the img/projects folder), and 2 link buttons that will link to the project site and the Github page. All of the items will be laid out using CSS Grid.

- Once again, I'll not go into details about the structure of the markup itself, since it's pretty straightforward, and is easily readable by viewing the '.html' file.

### Styling the 'My Work' page

We'll go to the 'main.scss' page and start styling the newly created page. We will select the main content items container and set `display: grid`. Right now the images that are embedded in the page are in their original size, and so we would want to shrink them to fir their container size, and so we'll set the width to a relative size.

```scss
.projects {
  display: grid;

  img {
    width: 100%;
  }
}
```

Next we will set the grid items. In here we won't need to use the `grid-template-areas`, as the original layout of the items on the page suit our needs, and so we will just set the column formation, and so we would like to have 3 columns with 1 fraction each. We'll also add a gap and border for the images with a simple layover, and we'll change the border color when we hover over it.

```scss
.projects {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 1rem;

  img {
    width: 100%;
    border: 2px #fff solid;
  }
}
```

Now we'll set some hover effects for the images, we'll set `opacity` and change to the `border-color`, including the `easeOut()` mixin.

- I also personally added a small `transform: scale()` effect, I think it makes the hover effect a little bit more cool this way.

```scss
.projects {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 1rem;

  img {
    width: 100%;
    border: 2px #fff solid;

    &:hover {
      opacity: 0.7;
      border-color: $secondary-color;
      @include easeOut();
      transform: scale(1.02);
    }
  }
}
```

### Styling the buttons

Next we would like to style the 2 buttons linking to the project site and the Github page. We will write the styles for the button separately from the styles of the `.project` container, as we'd like to have general specifications for buttons on the site. If in the future we would like to add more buttons, we would be able to refer to the general rules we'll set, and then we could 'export' these rules to more specific buttons, like the 2 buttons we have in this current page.

We'll go on and create style rules for the class `.btn`. Notably, we do not have any element with this class at the moment, but we would like to have something that holds 'general rules' that all the buttons we have now and in the future will be able to hold, and using SASS we can 'export' these rules to the specific items.

We will set `display: block` as we want each to act as a box. add some `padding`, `margin`, and set some hover effects.

```scss
.btn {
  display: block;
  padding: 0.4rem 1rem;
  border: 0;
  margin-bottom: 0.5rem;

  &:hover {
    background: $secondary-color;
    color: set-text-color($secondary-color);
  }
}
```

Now we can start styling our specific buttons we have in the 'work.html' page, which are `.btn-light` and `.btn-dark`. For these specific buttons to have the `.btn` class style rules, we will use the SASS `@extend .btn` which will "import" the rules from one element to a target element, and thus applying all the rules to it. Next we will add different color styles for these 2 buttons, one is darker and one lighter.

```scss
.btn-dark {
  @extend .btn;
  background: darken($primary-color, 50);
  color: #fff;
}

.btn-light {
  @extend .btn;
  background: lighten($primary-color, 80);
  color: #000;
}
```

### Adding responsiveness to the 'My Work' page

For that page to be responsive, we would like to change the layout of the items in the grid. At the moment, they're set to 3 columns, but if we will shrink the size of the display, it will look bad, and so we would like the columns to be bigger (4 columns on large screens) and fewer on smaller screen sizes (on the smallest - the items should be stacked upon each other).

And so, on the each size, we will change the `grid-template-columns`, the smaller the screen size get, the fewer columns we will have, up until the small screen media query, where the items get stacked upon each other since they are only set to `1fr`.

```scss
@include mediaXl {
  .projects {
    grid-template-columns: repeat(4, 1fr);
  }
}

// Large devices (Desktops & laptops)
@include mediaLg {
  .projects {
    grid-template-columns: repeat(3, 1fr);
  }
}

@include mediaMd {
  .projects {
    grid-template-columns: repeat(2, 1fr);
  }
}

@include mediaSm {
  .projects {
    grid-template-columns: 1fr;
  }
}
```

### Creating the 'Contact' page

This is the last page of our website, and it's a pretty simple one. It'll contain a few boxes that display the personal contact info. This time, we wll use CSS Flexbox to style the layout of the items in the page. We could also use CSS Grid of course, but for reviewing different styling options, we will use Flexbox instead.

- Again, I will not write down the specific markdown of the page, since it's very straightforward, just refer to the 'contact.html' page.

We will first style the container box of the page items. We would like to set the layout to `display: flex`, which will set the items into a flexbox layout. Next we will set the layout of the items: We'll `flex-wrap: wrap` so when the page shrinks the items will just automatically change their position by sliding down. And with this, we do not have to worry about responsiveness, as we change the screen size, the items automatically change positions, and on a small screen size, will be stacked upon each other due to the wrapping.

```scss
.boxes {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-evenly;
  align-items: center;
  margin-top: 1rem;
}
```

Next we will style the items themselves. We will add `font-size`, `border`, `margin`, `padding` and add the `easeOut()` mixin. Next we will add some hover effects, specially we would like to scale down the `padding` as it will give the boxes a nice scale effect. Also, we change the rules for the `<span>` upon a hover, so the text that is being wrapped will change his color from `$secondary-color` to a dark color, using the `set-text-color()` function.

```scss
.boxes {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-evenly;
  align-items: center;
  margin-top: 1rem;

  div {
    font-size: 2rem;
    border: 3px white solid;
    padding: 1.5rem 2.5rem;
    margin-bottom: 3rem;
    @include easeOut();

    &:hover {
      padding: 0.5rem 1.5rem;
      background: $secondary-color;
      color: set-text-color($secondary-color);

      span {
        color: set-text-color($secondary-color);
      }
    }
  }
}
```

# Part 7 - Deploying the site online

We will host the site in Github, using the GitHub Pages service, which is a free static website hosting service by Github. We will do that by creating a repository in Github, and later using the Github Pages terminal CLI we will deploy the site and make it go live.

### New Repo on Github

We will go to Github and create a new repository, I named mine 'Modern_Portfolio'. Now, since we've already made a `git init` and have committed all the changes so far, we can go ahead and add the site folder to the remote using `git remote add origin https://github.com/EliTu/Modern_Portfolio_By_Traversy_Media.git`, after that we can go ahead and use `git push -u origin master` to get all the files into the repo master branch.

### Deploying on Github Pages

First we will have to use npm to install a component named 'gh-pages', and so we will go on the terminal and type `npm install gh-pages`. Next we will go to our 'package.json' file and add `"homepage": "https://EliTu.github.io/Modern_Portfolio"` which will act as the URL to the homepage, and the gh-pages will know where to deploy the repo.

Next we will go to the `"scripts"` and under the `"sass"` script we will add `"deploy"` script, and it will run `"gh-pages -d dist"`, which will point to the directory to be deployed, which is of course the 'dist' directory.

After that, we can go to the terminal and type `npm run deploy` and it should be deploying the folder on the homepage. Upon success, we should receive a "published" message in the terminal.

### Custom Domain

If we don't like the default Github Pages domain we can customize the domain in the settings. Of course, to have a custom domain we would first need to register a domain in some domain registry site.