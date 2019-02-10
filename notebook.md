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
