# Part 3 - Rotating Menu Button & adding JavaScript

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
