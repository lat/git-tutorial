# Git CLI Tutorial
Git is a free and open-source version control system that utilizes branching to easily manage and maintain everything from the most complex enterprise coding projects to your school paper.

Did that make no sense? Good! That means you're in the right place.
___
## Getting Started
In order to use Git you must first install it from it's repository [here](https://git-scm.com/downloads).
There are a number of fancy third-party GUIs for Git, but for the sake of simplicity and brevity this tutorial will solely focus on Git for the Command Line. Follow the instructions provided at the link above and install Git for your corresponding system.

Moving forward this tutorial will also assume you have Git properly installed on your machine, which you can check by entering the terminal command:
    
    $ git --version
If the terminal yells at you about not understanding your command, then I highly reccomend you browse this [article](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) on how to properly install Git. If it instead spits out a version number then you're good to go.
___
## Your First Repo
A code repository, or 'repo' for short, is just a fancy way of saying the folder with all of your projects files in it. What makes a repo special is that Git tracks all of the changes you make to those files, so when you eventually mess something up you can go back to your version that actually worked. Let's go ahead and create our first repo now.

First, ensure that you're currently in the directory where you want to make a repository, you can list your current directory by using '**ls**', and then '**cd**' to change your current directory to your desired location. For example, below I am changing to a folder on my Desktop called 'git-tutorial'.

    $ cd C:\Users\x\Desktop\git-tutorial
Now that we're in the right place I can create a Git repo with the command:

    $ git init
    Initialized empty Git repository in C:/Users/x/Desktop/git-tutorial/.git/
You'll notice a new .git folder has been created within our folder. This folder is the heart of our git repository, it records and logs all the neccessary changes, deleting it will also delete our project history.

Let's actualy add some code to our codebase. How do we make sure Git logs any changes we've made? Well it's through the power of...

___
## Background On Branches
Some very smart people long ago found out that coding is hard, and its very common for our code to break, so they decided that it would be a good idea to separate our new and 
experimental code from our main tried and true code.

Below is an abstract representation of what a typical Git repo might look like. On each '+' a **Branch** is created. It branches off as we work and test. This happens until development finishes and we recombine or **Merge**-- represented by a '='-- back into our **Master** branch. 

                      / - - - - - - - - \ Dev Branch
    Master - - - - - + - - - - + - - - - = - = - - - - >
                                \ - - - - - / Other Dev Branch

By doing this we not only ensure the Master branch remains stable by providing us a work environment to change and edit anything we like, branches are also helpful if you and your smart friends are coding a project together. You work on implementing your own feature while all your friends work on theirs, and when you're ready you can **Merge** all the work you did back into the **Master** branch. 

Although in the case above we imagined that we merged all three branches, this isn't always the case. Sometimes development will continue on in separate branches without remerging for a very long time!

Now that we got that out of the way we can start adding some files to our repository. 

___
## First Files

First, let's add our files to the folder in which our .git file lives. I added a small shell script called **'script.sh'** to my **git-tutorial** folder, so now when I do **'ls'** : 

    C:\Users\x\Desktop\git-tutorial(master)
    $ ls
    script.sh

But this doesn't mean Git is tracking this file, it just means it's in the same folder. For example, if I type the command **'git status'** it says:

    C:\Users\x\Desktop\git-tutorial(master)
    $ git status
    On branch master

    No commits yet

    Untracked files:
    (use "git add <file>..." to include in what will be committed)
    script.sh

    nothing added to commit but untracked files present (use "git add" to track)

So let's actually track our files. We can do that by entering **'git add'** then the name of our file(s).

    $ git add script.sh

Now when I type **'git status'** I get

    C:\Users\x\Desktop\git-tutorial(master)       
    $ git status                                  
    On branch master                              
                                                
    No commits yet                                
                                                
    Changes to be committed:                      
    (use "git rm --cached <file>..." to unstage)
            new file:   script.sh         

Great, now Git knows we want to track the **'script.sh'** file. However, we're not done yet, we still have to **commit** the file. Right now it's technically in the **staging** area which you can just think of as the waiting room before the files are let in. The staging area is a place for us to get all of our files ready before we commit them all at once. Also note that sometimes the staging area is called the **'index'**.

Let's commit our **'script.sh'** file with **'git commit'**:

    C:\Users\x\Desktop\git-tutorial(master)
    $ git commit -m "added a startup script"
    [master (root-commit) 9b24fdb] added a startup script
    1 file changed, 0 insertions(+), 0 deletions(-)
    create mode 100644 script.sh

You'll also notice I appended '**-m**' to the end of the command, this allowed me to add a message with our commit to explain what it was we were changing.

Great, we now have a Master Branch with our file properly recorded in it. Now, let's create a branch to work on our brand new features. We can do this with the **'git branch'** and **'git checkout'** command. Branch, followed by a name will create a new branch with that name, and Checkout will switch to that branch. Often times you'll see this commands combined with **'git checkout -b'** which just means create a branch and then switch to it. For example, let's create a branch called NewFeature:

    C:\Users\x\Desktop\git-tutorial(master)
    $ git checkout -b NewFeature
    Switched to a new branch 'NewFeature'
Now if run our **'git branch'** command we can see our two branches and that we're working on our NewFeature branch.

    C:\Users\x\Desktop\git-tutorial(NewFeature)
    λ git branch
    * NewFeature
    master
So now that we're on our own branch let's add our new Feature files to our directory and then to our Git. I've went ahead and added my **'NewFancyFeature.py'** to our NewFeature branch with **'git add'** and then checked to make sure it worked with **'git status'**.

    C:\Users\x\Desktop\git-tutorial(NewFeature)
    $ git add NewFancyFeature.py

    C:\Users\x\Desktop\git-tutorial(NewFeature)
    $ git status
    On branch NewFeature
    Changes to be committed:
    (use "git restore --staged <file>..." to unstage)
            new file:   NewFancyFeature.py

Now it's only in the staging area, let's finalize our changes with **'git commit'**

    C:\Users\x\Desktop\git-tutorial(NewFeature)
    $ git commit -m "py file with new cool features"
    [NewFeature d164740] py file with new cool features
    1 file changed, 0 insertions(+), 0 deletions(-)
    create mode 100644 NewFancyFeature.py

Looking good! 
___
## Masterfully Merging
Let's pretend that the new features seem to be successful on our testing branch, let's add it to our master branch. We can do that with the **'git merge'** command, which will attempt to merge and combine our two separate branches.
Note this can get really messy and completed with merge-conflicts and failures and has been the source of many a sleepless night.

First let's switch back to our **'Master'** branch with:

    C:\Users\x\Desktop\git-tutorial(NewFeature)
    $ git checkout master
    Switched to branch 'master'

Now let's merge the **'master'** branch with our **'NewFeature'** branch where we've made all our changes. We do this with **'git merge'** followed by the name of the branch we want to merge it with:

    C:\Users\x\Desktop\git-tutorial(master)
    $ git merge NewFeature
    Updating 9b24fdb..d164740
    Fast-forward
    NewFancyFeature.py | 0
    1 file changed, 0 insertions(+), 0 deletions(-)
    create mode 100644 NewFancyFeature.py

Woohoo!

___
## Savy Stashes

Sometimes things can get messy and overwhelming. Merges aren't always clean, features don't always work, and it can be a good idea to go work on something else. That's what the **'git stash'** command is for. It allows us to stash whatever we're working on, saving it for later, but also letting us go work and edit something else on our project.

Let's say I have a new feature that I'm working on in a file called **'DifficultFeature.py'**. It kinda works but not really, and while it's in my staging area I definitely don't want to commit it to the master branch.
Let's stash this file with **'git stash'**:

    C:\Users\x\Desktop\git-tutorial(master)
    $ git status
    On branch master
    Changes to be committed:
    (use "git restore --staged <file>..." to unstage)
            new file:   DifficultFeature.py

As you can see the feature is in my staging area but has yet to be committed. This is the perfect time to stash it, so let's do just that with:

    C:\Users\x\Desktop\git-tutorial(master)
    $ git stash
    Saved working directory and index state WIP on master: d164740 py file with new cool features
We stashed the feature and it reverted us back to our most recent commit, which was **'NewFancyFeature'**.

Let's say some time has passed and we'd like to go back to work on what we had previously stashed. we can check it with **git stash list**' and see our previously stashed work:

        C:\Users\x\Desktop\git-tutorial(master)
    $ git stash list
    stash@{0}: WIP on master: d164740 py file with new cool features

Let's say we made some changes out our DifficultFeature.py and we're ready to go back and apply those changes to our master branch. We can do so with the **'git stash pop'** command. Pop will clear our stash and apply it to the master branch, if you don't want to clear your stash you can also use the apply command, for now we'll pop it with:


    C:\Users\x\Desktop\git-tutorial(master)
    $ git stash pop
    stash@{0}: WIP on master: d164740 py file with new cool features

And if we do the list command again we'll see it's gone:

    C:\Users\x\Desktop\git-tutorial(master)
    $ git stash list

That just about concludes this tutorial. Thank you so much, I hope you learned something!