# Sample Review Question

### Initialize a Git Repository
git init (This git command will help us to initialize git and we can do git operations)



### Add a file a.txt
First create the file with touch command (touch a.txt)
- git add . (Now, write this command to add that file. And make it come into staging area)



### Make a commit
- git commit -m "New file is created with name a.txt" (This commit will help the a.txt to save and move it to commit area, from where we can push into git remote repository. Here, we used -m option which is for commit message. It helps us to know what that commit is for)



### Create a branch called leaf
- git branch leaf (By writing this command, we will create a new branch with name 'leaf' and if we want to go into that branch we can type 'git checkout leaf' command)



### Add a file b.txt
- touch b.txt 
- git add . (We are creating file and adding in leaf branch)



### Create a second commit
- git commit -m "Another file is created with name b.txt in leaf branch" (We are moving b.txt from staging area to commiting area with a message)



### Merge leaf into master
- git checkout master (This command will help us to move into master branch)
- git merge leaf (This command will help us to merge leaf branch into master branch).

- Before merge, master branch contains only a.txt and leaf branch contains a.txt and b.txt file as well. Why, a.txt file is there in leaf branch means, when a branch is created it will be copy of master and we will do changes and merge those changes into master branch)
- After merge, both master and leaf branches will contains a.txt and b.txt files



## Checking understanding

### What is staging area?
The staging area is an intermediate area between working directory and commiting area. In this area there will be files and everything where changes are prepared before creating a commit. We will go into this area by 'git add .' command
- In Git, there will be three areas:
    - Working directory - In this area, we will create files, edit files and delete files that's why it called working where we work for our project 
    - Staging area - In this area, there will be files which are ready to be committed. We will use 'git add .' commit to go into this area
    - Commit area - It refers to the part of Git repository where permanently saved snapshots of staging area will be there.


### Where is HEAD right now?
After doing all above git commands, HEAD will be there at master branch.
 



