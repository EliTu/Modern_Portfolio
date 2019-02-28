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
