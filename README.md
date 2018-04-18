This is small `git` tutorial and a learning-by-doing workshop for new students joining Roboy in summer semester 2018.

Helpful resources:
 - Intro slides for this workshop are inside this repository
 - [GitHub git cheatsheet](https://services.github.com/on-demand/downloads/github-git-cheat-sheet.pdf)
 - [GitHub git interactive tutorial](https://try.github.io/)
 - [git - the simple guide](https://rogerdudler.github.io/git-guide/)


# Preparation
## Step -2: install software

Make sure `git` is installed on your system. On Ubuntu, you can install it with:  
`$ sudo apt-get install git-core`

## Step -1: get write access to this repository

Ask the guy who does this tutorial to give you write access. You will need it later.

## Step 0: find a team

To follow this workshop you will need a team of tree (or at least a team of two). 
Every team should have a unique number (or name). In the following workshop you will create a few branches. Always replace `xx` with your team name!

After you find a team and decide on a name, every team member gets one of the three roles assigned (`A`, `B` or `C`).
These roles will be used to specify the actions for every team member later in the workshop.

# Workshop
## Step 1: master branch for the team
Clone the repository:  
`$ git clone https://github.com/Roboy/roboy_git_tutorial_ss18.git` (roles: `A`, `B` and `C`)

Move into the new cloned directory:  
`$ cd roboy_git_tutorial_ss18` (roles: `A`, `B` and `C`)

In the next step, person `A` will create a new master branch for the team (the original master branch is protected in this workshop). 
When you create a new branch, you should give it a good name. 
In this workshop, name it `team-xx-master` (*replace `xx` with your team name!*). 
Use `checkout` with the `-b` option to create a new branch and switch to it at the same time:  
`$ git checkout -b team-xx-master` (roles: `A` only)

Now, push the new branch to the server so your team members `B` and `C` can use it as well:  
`$ git push --set-upstream origin team-xx-master` (roles: `A` only)

The team members can now update their repositories and work on the new branch:  
`$ git fetch`   (roles: `B` and `C` only)  
`$ git checkout team-xx-master`   (roles: `B` and `C` only)  
`$ git pull`   (roles: `B` and `C` only)


## Step 2: add your names
Now, let's simulate a project development. Inside the repository, you will find a `git_tutorial.html` file. 
Your team will simultaneously work on it and synchronize the code with `git`.

For smaller projects, everyone could just work on one branch. 
However, this is not recommended for larger projects, so we will use multiple branches and do it 'in a proper way'. 
Now, every team member creates a new branch for himself:  
`$ git checkout -b team-xx-name-a` (roles: `A` only)  
`$ git checkout -b team-xx-name-b` (roles: `B` only)  
`$ git checkout -b team-xx-name-c` (roles: `C` only)  

On your branch, edit `git_tutorial.html` and replace John Doe A/B/C with your name.
Do not change anything else. Tell `git` to add your changes with:  
`$ git add .` (roles: `A`, `B` and `C`)

Check if everything is correct with:  
`$ git status` (roles: `A`, `B` and `C`)

Commit your changes and give the commit a message with:  
`$ git commit -m "changed name A/B/C"` (roles: `A`, `B` and `C`)

Push your changes to the server with:  
`$ git push --set-upstream origin team-xx-name-a` (roles: `A` only)  
`$ git push --set-upstream origin team-xx-name-b` (roles: `B` only)  
`$ git push --set-upstream origin team-xx-name-c` (roles: `C` only)  

If you want, you can go on GitHub and check whether your changes were pushed to the server correctly.

Now, it is time to merge your branch into the team `team-xx-master` branch.
There are several ways to do it. For now, we will use a local merge.

Locally checkout the team master branch:  
`$ git checkout team-xx-master`   (roles: `A`, `B` and `C`)  

Locally merge your branch with the name change into the team master branch:  
`$ git merge team-xx-name-a` (roles: `A` only)  
`$ git merge team-xx-name-b` (roles: `B` only)  
`$ git merge team-xx-name-c` (roles: `C` only)  

Push the updated team master branch to the server:  
`$ git push`  (roles: `A` only)  

Before your team members `B` and `C` can push their new changes, they first need to get the latest changes from the server:  
`$ git pull` (roles: `B` only)  

The changes made by `A` should now be automatically merged with the changes made by `B`.
Git will suggest you a merge commit message and you don't have to change it in this workshop.
Now push the merged changes to the server:  
`$ git push` (roles: `B` only)  

Now we repeat the same steps for person `C` (pull, accept merge message and push):  
`$ git pull` (roles: `C` only)  
`$ git push` (roles: `C` only)  

Note that merging could be done by one person as well. The person would fetch all new branches from the server, merge them all on his computer locally and push the updated version to the server.

Once the last team member has pushed the updated team master branch, get all changes from the server with:  
`$ git pull`  (roles: `A`, `B` and `C`)  

## Step 3: change the background colour
Previously, every team member made a change that has no conflicts with other changes. Now, we will create a situation with conflicts and resolve them. 

Every team member creates a new branch:  
`$ git checkout -b team-xx-bg-a` (roles: `A` only)  
`$ git checkout -b team-xx-bg-b` (roles: `B` only)  
`$ git checkout -b team-xx-bg-c` (roles: `C` only)  

Now, edit the `git_tutorial.html` file and change the background colour. Every team member should change it to a different value to produce a conflict. 

Add your changes, commit them and push to the server:  
`$ git add .` (roles: `A`, `B` and `C`)  
`$ git commit -m "changed background"` (roles: `A`, `B` and `C`)  
`$ git push --set-upstream origin team-xx-bg-a` (roles: `A` only)  
`$ git push --set-upstream origin team-xx-bg-b` (roles: `B` only)  
`$ git push --set-upstream origin team-xx-bg-c` (roles: `C` only)  

So far you pushed the changes to different branches, so there are no merge conflicts right now. 
This is one of the biggest advantages of `git`: everyone can work on his own branch and doesn't have to worry about breaking something.

Now, let's merge all the changes in the team master branch again. 
This time, the same line (background colour) was modified, so we expect to have merge conflicts.
To make merging easier, one person (`B`) will merge everything locally.

First, you fetch a list of all branches from the server:  
`$ git fetch`   (roles: `B` only)  

Then, you checkout one branch at a time and pull the changes from the server:  
`$ git checkout team-xx-bg-a` (roles: `B` only)  
`$ git pull` (roles: `B` only)  
`$ git checkout team-xx-bg-c` (roles: `B` only)  
`$ git pull` (roles: `B` only)  

Finally, checkout the team master branch and merge the team-xx-bg branches:  
`$ git checkout team-xx-master`   (roles: `B`)  
`$ git merge team-xx-bg-a`   (roles: `B`)  

So far there was no conflict. However, the next step will produce one:  
`$ git merge team-xx-bg-b`   (roles: `B`)  

Resolve the conflict in the `git_tutorial.html` file. After resolving, commit the change:  
`$ git add .`   (roles: `B`)  
`$ git commit -m "merged versions A and B and resolved the conflict"`  (roles: `B`)  

Now, merge the final change made by `C`:  
`$ git merge team-xx-bg-c`  (roles: `B`)  

Resolve the conflict in the `git_tutorial.html` file again. 
After resolving, commit the change and push it to the server:  
`$ git add .`   (roles: `B`)  
`$ git commit -m "merged changes by C and resolved the conflict"`   (roles: `B`)  
`$ git push`   (roles: `B`)  

Finally, other team members can checkout the team master branch and pull the changes from the master:  
`$ git checkout team-xx-master`   (roles: `A` and `C`)  
`$ git pull`   (roles: `A` and `C`)  

