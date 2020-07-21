

## Step 1: Creating a local git "repository"

When creating a new project on your local machine using git, you'll first create a new repository (or often, 'repo', for short). 

To use git we'll be using the terminal. If you don't have much experience with the terminal and basic commands, check out [this tutorial](https://towardsdatascience.com/a-quick-guide-to-using-command-line-terminal-96815b97b955). 

> If you are using Windows I highly recommend using [Git Bash](https://gitforwindows.org/) or [Windows PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/overview?view=powershell-7) as both these tools are syntactically similar to Linux and Mac. Personally, I run Ubuntu on Windows using [Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/about) and [Windows Terminal](https://www.microsoft.com/en-us/p/windows-terminal/9n0dx20hk701#activetab=pivot:overviewtab). 

To begin, open up a terminal and move to where you want to place the project on your local machine using the cd (change directory) command. For example, if you have a 'projects' folder on your desktop, you'd do something like:

```sh
# arogya @ DESKTOP-U99TER7 in ~ [7:33:38] $ cd projects
# arogya @ DESKTOP-U99TER7 in ~/projects [7:33:53] $ cd mkdir sample-git-project
# arogya @ DESKTOP-U99TER7 in ~/projects/sample-git-project $ cd projects

```
You can now initialize a git repository in the root of the folder, by running the `git init` command:  

```sh
# arogya @ DESKTOP-U99TER7 in ~/projects/sample-git-project [7:34:13] $ git init
Initialized empty Git repository in /home/arogya/projects/sample-git-project/.git/
```

## Step 2: Adding a new file to your repository

Go ahead and add a new file to the project, using any text editor you like, or if you're using linux or mac, by running a [`touch` command](https://www.geeksforgeeks.org/touch-command-in-linux-with-examples/).

Once you've added or modified files in a folder containing a git repo, git will notice that changes have been made inside the repo. But, git won't officially keep track of the file (that is, put it in a commit - we'll talk more about commits next) unless you explicitly tell it to.

```sh
# arogya @ DESKTOP-U99TER7 in ~/projects/sample-git-project on git:master o [7:35:54] $ touch example-file.txt
# arogya @ DESKTOP-U99TER7 in ~/projects/sample-git-project on git:master x [7:38:18] $ ls
example-file.txt
```
After creating the new file, you can use the `git status` command to see which files git knows exist.

```sh
# arogya @ DESKTOP-U99TER7 in ~/projects/sample-git-project on git:master x [7:38:33] $ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        example-file.txt

nothing added to commit but untracked files present (use "git add" to track)
```

What this basically says is, "Hey, we noticed you created a new file called example-file.txt, but unless you use the 'git add' command we aren't going to do anything with it."

## Step 3: Your first "commit"

### What is a "commit"?

To me, a commit is both a snapshot and pit stop. I know this seems a little confusing, but bear with me.

A commit is a record of what files you have changed since the last time you made a commit. Essentially, you make changes to your repo (for example, adding a file or modifying one) and then tell git to put those files into a commit. Commits make up the essence of your project and allow you to go back to the state of a project at any point.

So, how do you tell git which files to put into a commit? This is where the staging environment or index come in. As seen in Step 2, when you make changes to your repo, git notices that a file has changed but won't do anything with it (like adding it in a commit).

To add a file to a commit, you first need to add it to the staging environment. To do this, you can use the `git add <filename>` command (see Step 3 below). Once you've used the git add command to add all the files you want to the staging environment, you can then tell git to package them into a commit using the `git commit` command. 

### Adding a file to the staging evironment

Add a file to the staging environment using the `git add .` command. 

```sh
# arogya @ DESKTOP-U99TER7 in ~/projects/sample-git-project on git:master x [7:41:27] $ git add .
```
Adding a "." after the `git add` command tells git to include everything in the present working directory to the staging environment. You can also choose to add individual files to the staging environment using `git add YOUR_FILENAME_HERE`

If you rerun the `git status` command, you'll see that git has added the file to the staging environment (notice the "Changes to be committed" line).  

```sh
# arogya @ DESKTOP-U99TER7 in ~/projects/sample-git-project on git:master x [7:41:36] $ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   example-file.txt
```

To reiterate, the file has not yet been added to a commit, but it's about to be.

### Performing the actual "commit"

It's time to create your first commit!

Run the command `git commit -m "Your message about the commit"` to commit your changes to the repo.

```sh
# arogya @ DESKTOP-U99TER7 in ~/projects/sample-git-project on git:master x [7:43:59] C:130 $ git commit -m "First commit FTW"
[master (root-commit) d640917] First commit FTW
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 example-file.txt
```

It is good practice to make sure that the message at the end of the commit is related to what the commit contains - maybe it's a new feature, maybe it's a bug fix, maybe it's just fixing a typo. Don't put a message like "asdfadsf" or "foobar". You'll have a hard time tracking your changes if the project evolves to a giant monster of a codebase.

## Step 4: Creating a "branch"

Now that you've made a new commit, let's try something a little more advanced.

Say you want to make a new feature but are worried about making changes to the main project while developing the feature. This is where [git branches](https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell) come in. 

Branches allow you to move back and forth between 'states' of a project. For instance, if you want to add a new page to your website you can create a new branch just for that page without affecting the main part of the project. Once you're done with the page, you can [merge](https://git-scm.com/docs/git-merge) your changes from your branch into the master branch. When you create a new branch, Git keeps track of which commit your branch 'branched' off of, so it knows the history behind all the files. 

Let's say you are on the master branch and want to create a new branch to develop your web page. Here's what you'll do: Run `git checkout -b <my branch name>`. This command will automatically create a new branch and then 'check you out' on it, meaning git will move you to that branch, off of the master branch. Let's do that now.

```sh
# arogya @ DESKTOP-U99TER7 in ~/projects/sample-git-project on git:master o [7:56:36] $ git checkout -b my-funny-branch
Switched to a new branch 'my-funny-branch'
```

After running the above command, you can use the `git branch` command to confirm that your branch was created:

```sh
# arogya @ DESKTOP-U99TER7 in ~/projects/sample-git-project on git:my-funny-branch o [7:56:48]
$ git branch


  master
* my-funny-branch
(END)
```
The branch name with the asterisk next to it indicates which branch you're pointed to at that given time. 

Now, if you switch back to the master branch and make some more commits, your new branch won't see any of those changes until you merge those changes onto your new branch.

To exit the funny looking screen, press `q`

## Step 5: Creating a "repository" on Github inside the **DAT/Artathon** organization account

If you only want to keep track of your code locally, you don't need to use GitHub. But if you want to work with a team, you can use GitHub to collaboratively modify the project's code. Since we're all working collaboratively on the DATArtathon Github organization, I recommend navigating to the organization's Github page and creating a repository there. 

To create a new repo on GitHub, log in and go to the [DATArtathon GitHub home page](https://github.com/datartathon). You should see a green 'New' button: 

<img src="https://github.com/datartathon/gitting-started/blob/master/images/datartathon.png?raw=true" width="600px"/>

After clicking the button, GitHub will ask you to name your repo and provide a brief description:

<img src="https://github.com/datartathon/gitting-started/blob/master/images/new_repo.png?raw=true" width="600px"/>

When you're done filling out the information, press the 'Create repository' button to make your new repo.

GitHub will ask if you want to create a new repo from scratch or if you want to add a repo you have created locally. In this case, since we've already created a new repo locally, we want to push that onto GitHub so follow the '....or push an existing repository from the command line' section: 

```sh
# arogya @ DESKTOP-U99TER7 in ~/projects/sample-git-project on git:my-funny-branch o [7:57:43] C:148 $ git remote add origin https://github.com/datartathon/sample-git-project.git
# arogya @ DESKTOP-U99TER7 in ~/projects/sample-git-project on git:my-funny-branch o [8:14:13] $ git push -u origin master
Username for 'https://github.com': arogyakoirala
Password for 'https://arogyakoirala@github.com':
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Writing objects: 100% (3/3), 227 bytes | 227.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/datartathon/sample-git-project.git
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.
```

You'll want to change the URL in the first command line to what GitHub lists in this section since your GitHub username and repo name are different.

## Step 6: "Push" your "branch" to the Github repo

Now we'll push the commit in your branch to your new GitHub repo. This allows other people to see the changes you've made. If they're approved by the repository's owner, the changes can then be merged into the master branch.

To push changes onto a new branch on GitHub, you'll want to run `git push origin yourbranchname`. GitHub will automatically create the branch for you on the remote repository:

```sh
# arogya @ DESKTOP-U99TER7 in ~/projects/sample-git-project on git:my-funny-branch o [8:16:12] $ git push origin my-funny-branch
Username for 'https://github.com': arogyakoirala
Password for 'https://arogyakoirala@github.com':
Total 0 (delta 0), reused 0 (delta 0)
remote:
remote: Create a pull request for 'my-funny-branch' on GitHub by visiting:
remote:      https://github.com/datartathon/sample-git-project/pull/new/my-funny-branch
remote:
To https://github.com/datartathon/sample-git-project.git
 * [new branch]      my-funny-branch -> my-funny-branch
```

You might be wondering what that "origin" word means in the command above. What happens is that when you clone a remote repository to your local machine, git creates an alias for you. In nearly all cases this alias is called "origin." It's essentially shorthand for the remote repository's URL. So, to push your changes to the remote repository, you could've used either the command: `git push git@github.com:git/git.git yourbranchname` or `git push origin yourbranchname`

(If this is your first time using GitHub locally, it might prompt you to log in with your GitHub username and password.)

If you refresh the GitHub page, you'll see note saying a branch with your name has just been pushed into the repository. You can also click the dropdown button that says 'master' to see your branch listed there.


<img src="https://github.com/datartathon/gitting-started/blob/master/images/branches.PNG?raw=true" width="900px"/>

## Step 7: Creating a "pull request"

A pull request (or PR) is a way to alert a repo's owners that you want to make some changes to their code. It allows them to review the code and make sure it looks good before putting your changes on the master branch.

Before we submit a pull request, let's try making some changes to the  `example-file.txt` within the `my-funny-branch` branch so that the two brances (master and my-funny-branch) are not identical.

To do this, open up `example-file.txt` write something on it, and save it.  


<img src="https://github.com/datartathon/gitting-started/blob/master/images/change_text.png?raw=true" width="900px"/>


Use the git status command to review changes.

```sh
# arogya @ DESKTOP-U99TER7 in ~/projects/sample-git-project on git:my-funny-branch o [8:27:36] $ git status
On branch my-funny-branch
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   example-file.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

Commit your change:

```sh
# arogya @ DESKTOP-U99TER7 in ~/projects/sample-git-project on git:my-funny-branch x [8:30:45] C:1 $ git add .

# arogya @ DESKTOP-U99TER7 in ~/projects/sample-git-project on git:my-funny-branch x [8:30:53] $ git commit -m "Modified example-file.txt"
[my-funny-branch 671e86c] Modified example-file.txt
 1 file changed, 1 insertion(+)

```

Push your changes to the remote branch:

```sh
# arogya @ DESKTOP-U99TER7 in ~/projects/sample-git-project on git:my-funny-branch o [8:31:03] $ git push origin my-funny-branch
Username for 'https://github.com': arogyakoirala
Password for 'https://arogyakoirala@github.com':
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 4 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 364 bytes | 364.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/datartathon/sample-git-project.git
   d640917..671e86c  my-funny-branch -> my-funny-branch
```

Now we are ready to open a pull request. Head over to the "Pull request" in your project, the page should tell you that `my-funny-branch` has new changes. Click the "Compare and pull request" button.


<img src="https://github.com/datartathon/gitting-started/blob/master/images/new_pull_request.PNG?raw=true" width="900px"/>

Finally, click the "Create pull request" button

<img src="https://github.com/datartathon/gitting-started/blob/master/images/create_pull_request.PNG?raw=true" width="900px"/>

## Step 8: "Merge" a pull request

This is what it looks like once you've submitted the pull request:

<img src="https://github.com/datartathon/gitting-started/blob/master/images/merge.png?raw=true" width="900px"/>

You might see a big green button at the bottom that says 'Merge pull request'. Clicking this means you'll merge your changes into the master branch.

Note that this button won't always be green. In some cases it'll be grey, which means you're faced with a merge conflict. This is when there is a change in one file that conflicts with a change in another file and git can't figure out which version to use. You'll have to manually go in and tell git which version to use.

Sometimes you'll be a co-owner or the sole owner of a repo, in which case you may not need to create a PR to merge your changes. However, it's still a good idea to make one so you can keep a more complete history of your updates and to make sure you always create a new branch when making changes.

Go ahead and click the green 'Merge pull request' button. This will merge your changes into the master branch.

<img src="https://github.com/datartathon/gitting-started/blob/master/images/merged.png?raw=true" width="900px"/>

When you're done, I recommend deleting your branch (too many branches can become messy), so hit that grey 'Delete branch' button as well.

You can double check that your commits were merged by clicking on the 'Commits' link on the first page of your new repo.



## Step 9: "Pull" changes back to the local machine.

Right now, the repo on GitHub looks a little different than what you have on your local machine. For example, the commit you made in your branch and merged into the master branch doesn't exist in the master branch on your local machine.

In order to get the most recent changes that you or others have merged on GitHub, use the `git pull origin master` command (when working on the master branch).

First we switch to the master branch.

```sh
# arogya @ DESKTOP-U99TER7 in ~/projects/sample-git-project on git:my-funny-branch o [8:32:02] $ git checkout master
Switched to branch 'master'
Your branch is up to date with 'origin/master'.
```

Then we pull the changes:

```sh
# arogya @ DESKTOP-U99TER7 in ~/projects/sample-git-project on git:master o [8:46:21] C:130 $ git pull origin master
Username for 'https://github.com': arogyakoirala
Password for 'https://arogyakoirala@github.com':
remote: Enumerating objects: 1, done.
remote: Counting objects: 100% (1/1), done.
remote: Total 1 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (1/1), 641 bytes | 641.00 KiB/s, done.
From https://github.com/datartathon/sample-git-project
 * branch            master     -> FETCH_HEAD
   d640917..843e57a  master     -> origin/master
Updating d640917..843e57a
Fast-forward
 example-file.txt | 1 +
 1 file changed, 1 insertion(+)
```

This shows you all the files that have changed and how they've changed.

Now we can use the git log command again to see all new commits.

## Step 10: We're done!

Congratulations! You've successfully made a PR and merged your code to the master branch.
