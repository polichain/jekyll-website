# jekyll-website
Just our website

# How to run it
Install jekyll and gems
Check how to install ruby. It depends on what OS is, please check the official documentation on https://www.ruby-lang.org/en/documentation/installation/ <br>

Install the dependencies.
```gem install bundler jekyll```

Clone this repo
```git clone https://github.com/polichain/jekyll-website```

### What you wanna do?
If you want to build it, just do
```jekyll build```

Also, ```jekyll``` has the feature of ```serve``` to a localhost.
``jekyll serve``

If you want to deploy it, remember that the usually called ``src`` folder is the ``_site``. In this repository we are using firebase to do so. See https://firebase.google.com/docs/cli for instructions.

# Submiting changes
Create a new branch, rebase it and then open the pull request. There are various ways to interact with git and github, but using remotes is the most common. 

Highly recommend using git-lens on VSCode or analogous to solve conflicts on rebase.