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

We will start with the right side, which is the nav menu. We will 0 the `margin` and the `padding`. We will set a background color to a darker version of the `primary-color` variable using the SASS `darken()` function (later I set it all inside an `rgba()` function to give it an opacity value).

Next we would like to style the opening transition effect ,as we want it to slide from the top, and so we will use `transform: translate3d()` values to achieve that effect. the `translate3d()` takes positioning parameters and moves in the selected item inside the container (also can be outside the container, as in our case), we will give an initial value of `(0, -100%, 0)` which will offset the nav-items box outside the page on the top side by default, and then when we will click on the menu button and the `.show` class will be applied, we will restore the values to the default `(0, 0, 0)` and then it will position the nav item box in its set position. We will also include our mixin of `easeOut()` to make the transition smooth.

```scss
&-nav {
  margin: 0;
  padding: 0;
  background: rgba(darken(primary-color, 5), 0.9);
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

We set the `background` as the `primary-color` (and I give it rgba() function for the opacity), include the mixin for the smooth transition and do the same thing with the `transform: translate3d()`, only this time we want this side of the menu to slide from the bottom, and so we set the Y-value at the opposite side of the nav side, and so the values will be set to `(0, 100%, 0)`, and by default the left side of the menu will be offset outside the viewport at the bottom, and only upon applying the `.show` class it will slide in from the bottom to its default position.

Next we would like to add in the portrait so the left side will have content. The portrait is an HTML `<div>`, and so we will select its class and give it an `background` with a `url()` of the image in our 'img' folder, next we will set its `width` and `height` to be smaller and give it a round cover using `border-radius` value of 50% and a solid `border`. Lastly, we will set `opacity` value of 1 in order for the image not to be transparent.

```scss
&-branding {
  background: rgba(primary-color, 0.9);
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
    border: solid 3px secondary-color;
    opacity: 1;
  }
}
```

### Styling the nav items

We want to set the nav items each off the screen as well, as eventually we want them to be transitioned into the screen with the container, after pressing on the menu button. So we will again set `transform: translate3d()` to achieve the desired effect, only this time we're on the X-axis, and so we would want to offset the nav-items off the screen to the right, and so we will give it a value of `(600, 0, 0)`. As usual we will include the `easeOut()` for the smooth-transition, and when the `.show` class is applied, we want to set it back to the default position. Lastly we set a special new class named `current` which will permanently 'mark' the current page (represented by the `<a>` tag) we're on with the `secondary-color`, by default its the home page.

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
    color: secondary-color;
  }
}
```

At this point the menu items are sliding in from the right, but the problem is that all of the items are sliding in at once, and it doesn't look as good as it can be, so we would like to give it the rule so that every item can slide in individually and with a small delay on each variable (that is being looped 4 times) and give it a 0.05 seconds delay. Like that, the nav items will come one by one with a small delay, and not all at once.

```scss
// Delay each nav item slide by 0.1 seconds - SASS for loop
@for x from 1 through 4 {
  .nav-item:nth-child(#{x}) {
    transition-delay: x * 0.05s;
  }
}
```

### Styling the links

Now we want to style the links of the nav items individually. We will display them as `inline-block` with a `relative` position, and also after the style options we will include the mixin. Upon a hover we will apply the `secondary-color`.

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
    color: secondary-color;
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
