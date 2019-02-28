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
