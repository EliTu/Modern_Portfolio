# Part 1 - Intro, Overview & SASS Workflow setup

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
