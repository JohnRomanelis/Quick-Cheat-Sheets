# GIT 
Based on https://product.hubspot.com/blog/git-and-github-tutorial-for-beginners

- git init : Initializes a repository on the local machine
- git status : See which files git knows exist and their state (commited or not)
- git add <filename> command : add a file to a commit
- git commit -m "Message about commit" : Creating a commit. The message is important to note the changes that are made during this commit
- git checkout -b <my branch name> : create a new branch
- git checkout <existing branch name> : switch between existing brances
- git branch : shows a list of existing brances. * indicates the current branch
- git remote add origin https... : connecting to a github repo. This repo is usually referenced as "origin".
- git push origin <branch name> : pushing commited files to github.
- git pull origin <branch name> : updating the current branch based on the changes that have been added on the github
- git log : see the new commits, after a pull operation
