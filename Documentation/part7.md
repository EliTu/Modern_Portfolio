# Part 7 - Deploying the Site Online

We will host the site in Github, using the GitHub Pages service, which is a free static website hosting service by Github. We will do that by creating a repository in Github, and later using the Github Pages terminal CLI we will deploy the site and make it go live.

### New Repo on Github

We will go to Github and create a new repository, I named mine 'Modern_Portfolio'. Now, since we've already made a `git init` and have committed all the changes so far, we can go ahead and add the site folder to the remote using `git remote add origin https://github.com/EliTu/Modern_Portfolio_By_Traversy_Media.git`, after that we can go ahead and use `git push -u origin master` to get all the files into the repo master branch.

### Deploying on Github Pages

First we will have to use npm to install a component named 'gh-pages', and so we will go on the terminal and type `npm install gh-pages`. Next we will go to our 'package.json' file and add `"homepage": "https://EliTu.github.io/Modern_Portfolio"` which will act as the URL to the homepage, and the gh-pages will know where to deploy the repo.

Next we will go to the `"scripts"` and under the `"sass"` script we will add `"deploy"` script, and it will run `"gh-pages -d dist"`, which will point to the directory to be deployed, which is of course the 'dist' directory.

After that, we can go to the terminal and type `npm run deploy` and it should be deploying the folder on the homepage. Upon success, we should receive a "published" message in the terminal.

### Custom Domain

If we don't like the default Github Pages domain we can customize the domain in the settings. Of course, to have a custom domain we would first need to register a domain in some domain registry site.)
