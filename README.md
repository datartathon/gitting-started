# gitting-started

Hi, and welcome to this brief introduction to the Git versioning system. 

As someone coming from a mechanical engineering background, my motivation for creating this resource from the fact that like most of us in this group, I have had a somewhat non-linear, non-traditional path to coding. My goal is to share what I've learned about how developers approach code management, and also talk about using GIT as not just a code management tool, but also an efficient approach to documentation and project management.


## A few things before we get started.


### `git` is a command line tool.

We've all dealt with command line tools in the past. As someone who grew up using Windows throughout my childhood, the strongest example I can think of is opening up MS-DOS (or Terminal) and navigating the present directory using commands like `cd`, `mkdir`, `dir`, etc. 

![MS DOS](https://github.com/datartathon/gitting-started/blob/master/dos.jpg?raw=true)

The alternative to command-line tools are GUIs, i.e. Graphical User Interfaces. If these two (GUIs and command-line tools), were to come head to head in a contest, GUI would steal the show in the "user-friendliness" category, whereas commad line tools would come as victor in "automation" and "server-side deployment". This is why, I found out, developers prefer command line tools: all actions can be sequentially arranged through text-based commands, which makes automation a walk in the park.  

> For all R enthusiasts out there, r-base is a command line tool, and RStudio is a GUI that invokes r-base commands depending on user interaction.

### `git` helps solve a real problem.

### `git` has a lot of jargon.

I wouldn't say that `git` is beginner friendly. It comes with a lot of jargon such as `repository`, `cloning`, `pulling from master`, `diff`, `merge-request`. My approach to dealing with them is by making analogies, which I will briefly expand in a bit.   


### `git` is a concept, Gitlab, Github, BItBucket etc. are just implementations of the `git` concept.

`git` was introduced to the world by Linus Torvalds, the same guy that invented Linux. When I first learned about him, I really admired him for his a genius, he created an open source OS that changed the world, and then created a mechanism where thousands of people could collaborate. However, over the years it has come to light that [working with the guy is a nightmare](https://www.newyorker.com/science/elements/after-years-of-abusive-e-mails-the-creator-of-linux-steps-aside), and now I'm not sure how to feel about the guy anymore.


## Installing git
Since there are a wide variety of lessons already dedicated to this topic, I've decided to save some time and screen-space, by pointing you to tutorials on the topic:

* [Install Git on Mac OS X](https://www.atlassian.com/git/tutorials/install-git#mac-os-x)
* [Install Git on Windows](https://www.atlassian.com/git/tutorials/install-git#windows)
* [Install Git on Linux](https://www.atlassian.com/git/tutorials/install-git#linux)

## Your first git project


### Step 1: Creating a local git `repository`

When creating a new project on your local machine using git, you'll first create a new repository (or often, 'repo', for short). 

To use git we'll be using the terminal. If you don't have much experience with the terminal and basic commands, check out [this tutorial](https://towardsdatascience.com/a-quick-guide-to-using-command-line-terminal-96815b97b955).

To begin, open up a terminal and move to where you want to place the project on your local machine using the cd (change directory) command. For example, if you have a 'projects' folder on your desktop, you'd do something like:

```
# arogya @ DESKTOP-U99TER7 in ~ [7:33:38] $ cd projects
# arogya @ DESKTOP-U99TER7 in ~/projects [7:33:53] $ cd mkdir sample-git-project
# arogya @ DESKTOP-U99TER7 in ~/projects/sample-git-project $ cd projects

```
You can now initialize a git repository in the root of the folder, by running the `git init` command:  

```
# arogya @ DESKTOP-U99TER7 in ~/projects/sample-git-project [7:34:13] $ git init
Initialized empty Git repository in /home/arogya/projects/sample-git-project/.git/
```

### Step 2: Adding a new file to your repo

Go ahead and add a new file to the project, using any text editor you like, or if you're using linux or mac, by running a [`touch` command](https://www.geeksforgeeks.org/touch-command-in-linux-with-examples/).

Once you've added or modified files in a folder containing a git repo, git will notice that changes have been made inside the repo. But, git won't officially keep track of the file (that is, put it in a commit - we'll talk more about commits next) unless you explicitly tell it to.

```
# arogya @ DESKTOP-U99TER7 in ~/projects/sample-git-project on git:master o [7:35:54] $ touch example-file.txt
# arogya @ DESKTOP-U99TER7 in ~/projects/sample-git-project on git:master x [7:38:18] $ ls
example-file.txt
```
After creating the new file, you can use the `git status` command to see which files git knows exist.

```
# arogya @ DESKTOP-U99TER7 in ~/projects/sample-git-project on git:master x [7:38:33] $ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        example-file.txt

nothing added to commit but untracked files present (use "git add" to track)
```

What this basically says is, "Hey, we noticed you created a new file called example-file.txt, but unless you use the 'git add' command we aren't going to do anything with it."

### Step 3: Your first `commit`

#### What is a `commit`?

To me, a commit is both a snapshot and pit stop. I know this seems a little confusing, but bear with me.

A commit is a record of what files you have changed since the last time you made a commit. Essentially, you make changes to your repo (for example, adding a file or modifying one) and then tell git to put those files into a commit. Commits make up the essence of your project and allow you to go back to the state of a project at any point.

So, how do you tell git which files to put into a commit? This is where the staging environment or index come in. As seen in Step 2, when you make changes to your repo, git notices that a file has changed but won't do anything with it (like adding it in a commit).

To add a file to a commit, you first need to add it to the staging environment. To do this, you can use the `git add <filename>` command (see Step 3 below). Once you've used the git add command to add all the files you want to the staging environment, you can then tell git to package them into a commit using the `git commit` command. 



#### Adding a file to the staging evironment

Add a file to the staging environment using the `git add .` command. Adding a "." after the `git add` command tells git to include everything in the present working directory to the staging environment.

```
# arogya @ DESKTOP-U99TER7 in ~/projects/sample-git-project on git:master x [7:41:27] $ git add .
```

If you rerun the `git status` command, you'll see that git has added the file to the staging environment (notice the "Changes to be committed" line).  

```
# arogya @ DESKTOP-U99TER7 in ~/projects/sample-git-project on git:master x [7:41:36] $ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   example-file.txt
```

To reiterate, the file has not yet been added to a commit, but it's about to be.

#### Performing the actual `commit`

It's time to create your first commit!

Run the command `git commit -m "Your message about the commit"` to commit your changes to the repo.

```
# arogya @ DESKTOP-U99TER7 in ~/projects/sample-git-project on git:master x [7:43:59] C:130 $ git commit -m "First commit FTW"
[master (root-commit) d640917] First commit FTW
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 example-file.txt
```

It is good practice to make sure that the message at the end of the commit is related to what the commit contains - maybe it's a new feature, maybe it's a bug fix, maybe it's just fixing a typo. Don't put a message like "asdfadsf" or "foobar". You'll have a hard time tracking your changes if the project evolves to a giant monster of a codebase.

### Step 4: Creating a `branch`

### Step 5: Creating a `repository` on Github

### Step 6: `Push` your `branch` to the Github repo

### Step 7: Creating a `pull request`

### Step 8: `Merge` a pull request

### Step 9: `Pull` changes back to the local machine.




