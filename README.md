# jekyll-website
Just our website
<br>
<br>

# Instructions
## What does your computer need to run it?

Jekyll and Gems, both from Ruby, and this repository cloned.

> Obs.: If you don't have rubby installed, install it. The procedure depends on what OS you're using, please check the official documentation on https://www.ruby-lang.org/en/documentation/installation/ <br> 

To install the dependencies use:  <br>
```gem install bundler jekyll```

Then, clone this repo using: <br>
```git clone https://github.com/polichain/jekyll-website```

### How to run it?

1. Once you have everything we need, you can, inside the repository, use: "```bundle install```" to install all the dependencies the project need;

2. To build it, just do "```bundle exec jekyll build```", don't mind the warnings, they come from an imported package and **should not** be modified.

3. Finally, for running locally ```jekyll``` has the feature of ```serve```. So you can use: "```bundle exec jekyll serve```" and the server should start at port 4000 on your localhost.

## How to deploy it
?
If you want to deploy it, remember that the usually called ```src``` folder is the ```_site```. In this repository we are using firebase to do so. See https://firebase.google.com/docs/cli for instructions.

# Submiting changes
Create a new branch from ```base-project```, make your changes, when done just rebase it and then open the pull request. There are various ways to interact with git and github, but using remotes is the most common. 

Highly recommend using git-lens on VSCode or analogous to solve conflicts on rebase.

# Common problems

## Are you getting a timeout error when installing dependecies with gem?
You might have issues with IPV4 VS IPV6, Check this solution:
https://www.appsloveworld.com/ruby/100/18/timeout-when-installing-ruby-gems

## You have the dependencies installed, but your terminal doesn't seem to know it?
- Try restarting the terminal;
- If it didn't work you can resolve the local PATHs variables (recommended), or use ```sudo gem install bundler jekyll``` on Linux or run the terminal with administration privileges and use the regular command. Obs.: Note that this is not the best solution.
