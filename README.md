Training
========

Introduction
------------

This is the Git Training program that will prepare you for using the main project. To be given access to the main repository, you must first complete this training program. This tutorial expects that the tools and software have already been installed on your local computer.

For this tutorial, edits to files can be done through explorer/notepad, but any commands should be run in the "Git Bash" program. This will give you a greater understanding and help you learn any other tools in the future as they will use the same terms

### Prerequisite

Install git (https://git-scm.com/download/win)

I personally use TortoiseGit GUI tool for git where I can perform all the action by UI without knowing the command name (But I strongly suggest you should do this exercise with git bash command line that will give you an understanding of various git commands) https://tortoisegit.org/download/

Git extension for visual studio (dont require for this exersie but can be helpful when you started working on the real projects)

Tutorial Part 1
---------------

### 1. Fork

Your first step should be to create a fork of this project. By creating a Fork, you are creating a public copy of this repository that you have read and write access to.

To create your fork, press the `Fork` button on the top right of this page. You should now be viewing this page from your local fork (`github.com/Username/Training`)

### 2. Clone

Your next step is to create a local copy of this repository on your computer. This will give you a full copy of the repository with the ENTIRE history from the start to the current state.

To clone this repository, at the top of the page, press the SSH button and copy the link. Then perform the following command

	git clone copied_url

This will copy the repository with it's entire history to your local machine. Now move in to the repository by typing:

	cd Training

### 3. Change

We will now create a simple change to one of the files. Under the Traininng/Tutorial folder, there is a file called `changeme.txt`. Add your name to this document in the appropriate location and save it.

If you now run the status command, you should see that there is a modified file.

	git status

This command will also inform you of your current branch and any untracked files.

### 4. Add

Once you have made a change, you need to add it to the staging area so that it can be committed. This allows you to pick and choose which files you want sent when you create your commit.

To add the changes you created in the last step, type:

	git add Tutorial/changeme.txt

if you now run the status command (git status), you will see that the file has been staged.

### 5. Commit

We now want to register this change as a commit in the git repository. This encapsulates all the changes you have made and creates a snapshot of the current state of your working directory. To do this type:

	git commit -m "This is my first commit"

This will now take a snapshot of the directory excluding any files not in the staging area.

Note: Some tools will perform the `Add` and `Commit` commands at the same time.

### 6. Push

Now you can send these changes to the github server so that they are saved offsite. This helps ensure that you don't lose work and can be performed as much as you want! Since your repository does not effect anyone else's, you don't need to worry about sending partial change sets to the server. 

To send your commit and sync the online repository to your local one, type:

	git push origin master

`origin` is the name of the remote (see the documentation) and `master` is the name of the branch you want to send. Both of these topics will be covered more in-depth shortly.

Once the command is sent, you can see that the github pages that corresponds to your repository is updated and shows a summary of the change set.

Tutorial Part 2
---------------

Please run the following command for part 2 of the tutorial

### 7. Branching

One of the great feature of git is the ease of which you can create new branches. Branching helps keep your development streams in seperate contexts so that you can work on several features or bug fixes in parallel.

We will now create a new branch. To do this, type the following command (replacing `your_username` with your github username: 

	git branch feature-your_username

This creates a new context that can be switched to at any time. To get a listing of all branches present in the repository, you can type:

	git branch

### 8.Checkout

Now that the branch is created, you should switch to it. To do this, type:

	git checkout feature-your_username

You should get a message that informs you that you have changed branches. Any commits created in this branch will not effect any others until you merge it.

### 9a. Change (Adv.) Part 1

We will now explore an important concept related to branches and changes.

Staying on the branch that you created in step 7/8, open the Tutorial/changeme.txt file and add the number 1 beside your username.

Now switch to the develop branch (without committing)

	git checkout develop

You should see that there is a message that says `M	Tutorial/changeme.txt`. This means that you brought the untracked file with you when you switched branches.

This is an important concept to understand. When you change branches, any changes that are not committed will follow you so that you do not lose them. This can however cause issues if you do not want that change in the branch you are switching to. There are several ways to deal with this, but the easiest way to to make sure you commit all of your files before switching branches.

Reset the file by typing:

	git checkout Tutorial/changeme.txt

### 9b. Change (Adv.) Part 2


Switch back to the branch you created earlier.

	git checkout feature-your_username

Under the Tutorial directory, create a new folder named with your username. In that folder create a file called: `README.md`

In that file, add the following text

	Hello Github! 
	=============

Save your file and exit out of your text editor.

Add the file

	git add Tutorial/your_username/README.md

Commit the file

	git commit -m "Added my new file"

Now if you switch branches you will see that this change does not follow you.

### 10. Pushing a branch

We will now push your branch to the online repository. This will save the individual branch to the online server. To do this, type:

	git push origin feature-your_username

Great, you've now pushed your branch!

### 11. Remotes

Your branch should now have been successfully push to github. If this were a complete feature, you'd now want it to be accepted and added to the blessed repository so that other users could grab your changes. However, you first need to sync your develop and feature branch with the blessed develop branch to ensure that there will not be merge conflicts. To do this, you first need to added a new remote location for the blessed branch. Type:

	git remote add upstream git@github.com:{{organizatio or personal git username}}/Training.git

This command adds a new remote location called `upstream` for the url provided. The convention is to call the blessed repository upstream. For any other remotes you choose to add (that link to other developers for example) you may call it what ever you wish.

### 12. Fetch

With the new remote added you now need to grab all of the updates. To do this type:

	git fetch upstream

This pulls the develop branch on to your machine.

### 13. Merge

The new commits that were added to the blessed repository's develop branch are now on your system, but you still need to merge them in. To do this, first switch to your develop branch:

	git checkout develop

Now you need to merge the files in. Type:

	git merge upstream/develop

This specifies that you want the upstream/develop branch merged in to the current branch that you have cheked out. The target for the merge will always be the current branch you have checked out.

### 14. Pull

Sometimes it's good be be able to to the fetch and merge as individual steps. Most times, you will want to perform that all at once. To do that, you can type:

	git pull upstream develop

The merge or pull command will automatically create a new commit in your repository. Once complete, you should push that commit to your repository.

	git push origin develop
	
### 15. Merge (Adv.)!

You've updated your develop branch to match that of the blessed repository, but you still need to update your feature branch. To do this, you will first need to checkout your branch:

	git checkout feature-your_username

Next, you will merge develop into this branch:

	git merge develop

This ensures that all of the latest commits in develop are applied to your feature branch.

	Note: In this tutorial, your feature branch will already be up to date and and nothing will happen. 
	In the wild, you may receive merge conflicts at this stage. If you do, don't panic! You can either
	fix them manually or use a 3 way merge gui tool (TortiseGit is great for this) to resolve the conflicts.
	**Once the conflicts are fixed, make sure that you commit!** You can read more about this in the 
	documentation.

Finally, push the change so that you will be able to create a pull request from the merged version

	git push origin feature-your_username
	
	Why merge to develop instead of straight to your feature branch? The main reason for this is to ensure 
	that your develop branch is aways up to date. There are several other benefits as well.
	
### 16. Pull Requests

Your branch should now have been successfully push to github.  Any time you want a full feature added to the blessed repository, you need to create a `pull request`. This sends a message to the repository managers that contains a summary of your changes and an optional message to go along with it. For the best practise, you will always create pull-requests from your feature branch. Failure to do so will result in a rejected pull request.

To start a pull request, first change your branch on the github.com web interface using the dropdown menu at the top left. Select your feature-your_username branch and then press the press the `Pull Request` button at the top of the page. Once you have pressed it, ensure that the top line says that you are creating the request **into** `{{{{organizatio or personal git username}}}}:develop` and **from** `YourUsername:feature-your_username`. If this is not correctly set, press teh `Change Commits` button and set them appropriately. Add a message of **"Please accept my pull request!"** and press the send pull request button.

This will inform the managers that you have a change set that you want merged.

	Note: it is your responsibility to ensure that there are no merge conflicts with your pull requests. 
	You should always merge develop in to your feature branch before creating a pull requests to ensure that
	your branch will merge cleanly. 
	Failure to do so could result in a rejected pull request.

Complete
--------

Don't panic if you still having difficulty understanding a few of the advance commands like merge, creating upstream or rebase since some of the GUI can have a very descriptive user interface. As long as you know what is push, pull, fetch and Branch then you can at-least head start on the project.