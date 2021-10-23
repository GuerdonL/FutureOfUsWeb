# Future Of Us Website Development
[![Netlify Status](https://api.netlify.com/api/v1/badges/b654c94e-08a6-4b79-b443-7837581b1d8d/deploy-status)](https://app.netlify.com/sites/gatsby-starter-netlify-cms-ci/deploys)

## Getting Started as a Contributor
### Operating System
This project is best worked on using a linux distribution, preferably a debian or ubuntu based one (Ubuntu recommended). That said, MacOS will work is you install <a href='https://brew.sh/'><p>homebrew</p></a> and are willing to do the research to translate the below commands from apt/bash. 
Windows is the worst OS for the job because it isn't unix based, but can be made to work with 

<a href='https://docs.microsoft.com/en-us/windows/wsl/install'><p>Windows Subsystem For Linux (WSL)</p></a> or manual installation of git bash and all other tools (wsl is vastly preffered as it should mirror native ubuntu well).

It is reccomended that you use some sort of environmental isolation, such as a vm or sandbox. Virtual machines are likely more beginner friendly, but may be severly limiting in terms of system resources if you opt not to use a type 1 hypervisor (e.g. virtualbox may not be good enough, research type 1 hypervisors like qemu).


### How This Project is Arranged
This project uses the gatsby framework as a static site generator that automates the process of loading html and then javascript. This approach allows for fast load times and SEO (html is more searchable and therefore SEO friendly) but also an extremely fast and responsive site with js and react components. 

The workflow of gatsby involves constructing a basic page layout in html, and then wrapping the html in, or injecting the html with, react components, which define layouts and interactions. We then style the react components with CSS in another file that links with the react file to make a cohesive component (ex. card.js links with card.css to create one styled component). Gatsby also acts as a system for plugins, such as stripe etc. which can be integrated into the site.

Once a change has been made to the site, you will make a pull request to merge your development branch back to the main branch where the website codebase is maintained. Upon approval of the pull and merger with the main branch, the entire codebase will be rebuilt in our CMS (content management system) Netlify-cms and deployed on Netlify proper, meaning there is always a deployed development site with the most recent changes.

We also will use Yarn to manage dependencies, so you should have to do minimal manual dependency management. That said, messing up a dependency is easy to do, and easy to overlook. If you then get the dependency pushed and merged, bad things can happen. Please be careful with your dependencies! (this is why isolated environments are recommended above).

### Cloning and Dependencies
[The following is a command guide for ubuntu and debian based systems. WSL should work with this if it uses the default Ubuntu version or a deb based distro]

If you do not have git or wget installed, do so now: 

```
sudo apt install git wget
```

Now we will install the Node Version Manager tool, which allows us to easily control our version of node.

```
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
```

Restart the terminal to apply changes.
Then install node version 14 and switch to the installed version:

```
nvm install 14 && nvm use 14
```
Now we will install gatsby version 2, netlify-cli, and yarn. These three are our main development tools.

```
npm install -g gatsby@2.32.0 netlify-cli yarn
```
[Note that getting 20 to 30 warnings is the expected behavior, many of these are simply skipping the optional dependencies for other operating systems. These can safely be ignored, if you get errors or a failed installation something has actually gone wrong.]

Now that everything is installed let's clone and enter the repository:

```
git clone https://github.com/GuerdonL/FutureOfUsWeb.git
cd FutureOfUsWeb
```

Now we run yarn to sync dependencies on our system to those already specified in the project:

```
yarn
```
[more warnings expected, although this is a likely step to run into real errors on]

And finally we can run the development build of the project:

```
netlify dev
```
[This hosts the *local* version of the develoment site on localhost, port 8888. It should launch your defualt browser to view the site, but if not just open a browser and navigate to <a href='http://localhost:8888/'>http://localhost:8888/</a>]
  
Changes you make to the local version of the website code will now be automatically displayed in the browser in real time (each time you save a file), for most modern browsers. Otherwise, refreshing the page will show your changes. It is a good idea to use chrome for this purpose, as it is the main browser we are developing for. Your pr's (pull requests) will however be tested on all the main browsers (e.g. chrome, safari, firefox, edge 🤮) so it is a good idea to test on as many of these as you can before making a pr, to ensure your pr goes smoothly.
  
## Development Environment

The general reccomendation for and IDE (Integrated Development Environment) is <a href='https://code.visualstudio.com/'>VSCode</a> simply because it has an extremely large library of plugins that allow for good syntax highlighting, autocomplete, language support, etc.. [note, VSCode is different than Visual Studio] 

If you would like to *really* learn something useful during this project, I suggest trying to set up either neovim with a terminal multiplexer like tmux or using emacs (you'll also want a fuzzy finder like fzf). Both of these have a pretty extreme learning curve and you will need to manually install support for things that vscode can do in a plug-and-play style. That said they will hugely boost your productivity if you ever do master them. Plus neovim will make you look like a hacker from a bad action movie. (This is mainly a reccomendation for linux users, if you want to learn something and aren't a linux user, just learn linux.)

  
## Debugging

As known errors occur in the cloning and contrib process this section will be updated. 

# CONTRIBUTING

This project uses the a hybrid trunk-based development and feature branch workflow version control system. This means that small teams (likely you and one partner) will create a new branch from main when you begin work on a new react component, page layout, or other extremely small scale feature.  You will then commit this branch centrally, and the non-commiting partner will also switch to this branch. You will then work on it together, each puching changes at frequent intervals to remain in sync with each other. Once you complete the smallest scale version of the complete feature, you make a pull request and start on the next small scale feature. This means you are mergining with the main branch as often as possible while not introducing broken code to main, which approximates a Continuous Integration(CI) workflow.
For example, you may create and merge a simple react component, then create and merge the css styling for that component, and finally create and merge the implementation of that react component in one of the exisiting page layouts. Each of these is a *seperate* feature, and a *seperate* branch. In other words, each branch should be for a different functional atomic feature, that is the smallest a feature can possibly be while still being a functional piece of code.
