---
title: Git Tutorial
tags:
  - Git
categories:
  - Git
abbrlink: 15074
date: 2018-01-28 13:33:32
---

## Mac/Linux Setup

### Installing Git

Here is a general installation on Mac/Linux. If you ar using Windows, then enjoy yourself.
Git is actually installed on MacOS, but we'll be reinstalling it so that we'll have the newest version:

- go to [Git](https://git-scm.com/downloads)
- download the software for Mac
- install Git choosing all of the default options

### First Time Git Configuration

Before you can start using Git, you need to configure it. Run each of the following lines on the command line to make sure everything is set up.

```bash
# sets up Git with your name
git config --global user.name "<Your-Full-Name>"

# sets up Git with your email
git config --global user.email "<your-email-address>"

# makes sure that Git output is colored
git config --global color.ui auto

# displays the original state in a conflict
git config --global merge.conflictstyle diff3

git config --list
```

### Git & Code Editor

The last step of configuration is to get Git working with your code editor. Below are three of the most popular code editors.

Atom Editor Setup

```bash
git config --global core.editor "atom --wait"
```

Sublime Text Setup

```bash
git config --global core.editor "'/Applications/Sublime Text 2.app/Contents/SharedSupport/bin/subl' -n -w"
```

VSCode Setup

```bash
git config --global core.editor "code --wait"
```

## Create a Git Repo

### Create a Repo from Scratch

```bash
mkdir -p git-practice/new-git-project && cd $_
```

Use `git init` to initialize a empty new empty Git repository.

.Git Directory Contents

Here's a brief synopsis on each of the items in the .git directory:

- config file - where all project specific configuration settings are stored.
- description file - this file is only used by the GitWeb program, so we can ignore it
- hooks directory - this is where we could place client-side or server-side scripts that we can use to hook into Git's different lifecycle events
- info directory - contains the global excludes file
- objects directory - this directory will store all of the commits we make
- refs directory - this directory holds pointers to commits (basically the "branches" and "tags")

### Clone An Existing Repo

Clone from URL

```bash
git clone https://github.com/udacity/course-git-blog-project
```

Clone with rename

```bash
git clone https://github.com/udacity/course-git-blog-project blog-project
```

## Determine A Repo's Status

```bash
git status

On branch master
Your branch is up-to-date with 'origin/master'.
nothing to commit, working directory clean
```

1. On branch master – this tells us that Git is on the master branch.
2. Your branch is up-to-date with 'origin/master'. – Because git clone was used to copy this repository from another computer, this is telling us if our project is in sync with the one we copied from. We won't be dealing with the project on the other computer, so this line can be ignored.
3. nothing to commit, working directory clean – this is saying that there are no pending changes.

## Git Log Command

### Use Git Log

```bash
git log
```

By default, this command displays:

- the SHA
- the author
- the date
- the message

It will display the log in `less` mode:

to scroll down, press

- j or ↓ to move down one line at a time
- d to move by half the page screen
- f to move by a whole page screen

to scroll up, press

- k or ↑ to move up one line at a time
- u to move by half the page screen
- b to move by a whole page screen

press q to quit out of the log (returns to the regular command prompt)

1. Use git log to find the commit that has a SHA that starts with f9720a. Who made the commit?
2. Use git log to find the commit with the SHA that starts with 8aa6668. What is the message for that commit?
3. Use git log to find the commit with the SHA that starts with f9720a9. When was that commit made?
4. Use git log to find the commit that has the message Set article timestamp color. Which commit belongs to that SHA? Provide the first 7 characters of the SHA.

### Change Git Log Displays

1. the SHA - git log will display the complete SHA for every single commit. Each SHA is unique, so we don't really need to see the entire SHA. We could get by perfectly fine with knowing just the first 6-8 characters. Wouldn't it be great if we could save some space and show just the first 5 or so characters of the SHA?
2. the author - the git log output displays the commit author for every single commit! It could be different for other repositories that have multiple people collaborating together, but for this one, there's only one person making all of the commits, so the commit author will be identical for all of them. Do we need to see the author for each one? What if we wanted to hide that information?
3. the date - By default, git log will display the date for each commit. But do we really care about the commit's date? Knowing the date might be important occasionally, but typically knowing the date isn't vitally important and can be ignored in a lot of cases. Is there a way we could hide that to save space?
4. the commit message - this is one of the most important parts of a commit message...we usually always want to see this

What could we do here to not waste a lot of space and make the output smaller? We can use a flag.

The git log command has a flag that can be used to alter how it displays the repository's information. That flag is --oneline:

```bash
git log --oneline
```

### Viewing Modified Files

The git log command has a flag that can be used to display the files that have been changed in the commit, as well as the number of lines that have been added or deleted. The flag is --stat ("stat" is short for "statistics"):

```bash
git log --stat
```

1. how many files were modified in the commit with the SHA 6f04ddd?
2. How many files were modified in the commit with the SHA 8d3ea36?
3. How many lines of code were deleted in index.html in the commit with the SHA 8d3ea36?

### Viewing File Changes

The git log command has a flag that can be used to display the actual changes made to a file. The flag is --patch which can be shortened to just -p:

This command adds the following to the default output:

- displays the files that have been modified
- displays the location of the lines that have been added/removed
- displays the actual changes that have been made

```bash
git log -p
```

1. look at the commit with the SHA 50d835d. What line number in app.css should you start looking at to see what has been changed?
2. Using git log and any of its flags, what code was added in by commit 4a60beb?
3. git log --stat and git log -p are both really helpful commands. Wouldn't it be great if we could have both of their output at the same time?
4. What does the -w flag do to the patch information?

### Viewing A Specific Commit

You must be tired with the scrolling of the previous practices, how about supply the SHA of a commit as the final argument for all of these commands?

```bash
git log -p fdf5493
```

It still show other commits when scrolling.

The other command that shows a specific commit is git show:

```bash
git show fdf5493
```

The git show command will show only one commit.
By default, git show displays:

- the commit
- the author
- the date
- the commit message
- the patch information

1. How many rulesets are added to the CSS by commit 8d3ea36?
2. There's a commit with the message "Convert social links from text to images". How many files were changed by this commit?
3. Look at commit fdf5493. What's the first HTML heading element that's added by this commit?

## Add Commits

### Git Add

Make a `new-git-project` directory, and `cd` into it, then `git init` it.

First, create a file named `index.html`, and fill it with some starter code:

```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <title>Blog Project</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <meta name="description" content="">
    <link rel="stylesheet" href="css/app.css">
</head>
<body>

    <script src="js/app.js"></script>
</body>
</html>
```

Things to note, the code references a CSS file and a JavaScript file.

Now create the CSS and JavaScript files. You can leave both of these files empty. We'll add content to them in a bit.

We just made a number of changes to the repository by adding files and content. It's time to do a quick check-in with Git:

```bash
git status
```

The Git noticed that there are some changes in the repository, so let's stage those files.

```bash
$ git add index.html css/app.css js/app.js
# Same as
$ git add .
```

When you use:

```bash
git status
```

You can find that:

```bash
use "git rm --cached <file>..." to unstage
```

### Git Commit

```bash
# check your default commit editor
git config --global core.editor
git commit
# Or just with -m flag
git commit -m "Initial commit"
```

Now add this just inside the body tag in index.html:

```html
<header>
    <h1>Expedition</h1>
</header>
```

```bash
git status
git add .
git commit
```

### How to write the commit message

The goal is that each commit has a single focus. Each commit should record a single-unit change. Now this can be a bit subjective (which is totally fine), but each commit should make a change to just one aspect of the project.

Now this isn't limiting the number of lines of code that are added/removed or the number of files that are added/removed/modified. Let's say you want to change your sidebar to add a new image. You'll probably:

- add a new image to the project files
- alter the HTML
- add/modify CSS to incorporate the new image

A commit that records all of these changes would be totally fine!

Conversely, a commit shouldn't include unrelated changes - changes to the sidebar and rewording content in the footer. These two aren't related to each other and shouldn't be included in the same commit. Work on one change first, commit that, and then change the second one. That way, if it turns out that one change had a bug and you have to undo it, you don't have to undo the other change too.

Do

- do keep the message short (less than 60-ish characters)
- do explain what the commit does (not how or why!)

Do not

- do not explain why the changes are made (more on this below)
- do not explain how the changes are made (that's what git log -p is for!)
- do not use the word "and". If you have to use "and", your commit message is probably doing too many changes - break the changes into separate commits. e.g. "make the background color pink and increase the size of the sidebar" The best way that I've found to come up with a commit message is to finish this phrase, "This commit will...". However, you finish that phrase, use that as your commit message.

### Git Diff

The `git diff` command can be used to see changes that have been made but haven't been committed, yet.

### Having Git Ignore Files

The `.gitignore` file is used to tell Git about the files that Git should not track. This file should be placed in the same directory that the `.git` directory is in.

[gitignore.io](https://www.gitignore.io/) is a good tool to generate `.gitignore` file.

## Tagging, Branching, amd Merging

### Tagging

The command we'll be using to interact with the repository's tags is the git tag command:

```bash
git tag -a v1.0
```

```bash
This will open your code editor and wait for you to supply a message for the tag. How about the message "Ready for content"?

CAREFUL: In the command above (git tag -a v1.0) the -a flag is used. This flag tells Git to create an annotated flag. If you don't provide the flag (i.e. git tag v1.0) then it'll create what's called a lightweight tag.

Annotated tags are recommended because they include a lot of extra information such as:

the person who made the tag
the date the tag was made
a message for the tag
Because of this, you should always use annotated tags.
```

After saving and quitting the editor, nothing is displayed on the command line. So how do we know that a tag was actually added to the project? If you type out just git tag, it will display all tags that are in the repository.

### Branching

The git branch command is used to interact with Git's branches:

```bash
git branch
```

It can be used to:

- list all branch names in the repository
- create new branches
- delete branches

### Create A Branch

To create a branch, all you have to do is use git branch and provide it the name of the branch you want it to create. So if you want a branch called "sidebar", you'd run this command:

```bash
git branch sidebar
```

### The git checkout Command

Remember that when a commit is made that it will be added to the current branch. So even though we created the new sidebar, no new commits will be added to it since we haven't switched to it, yet. If we made a commit right now, that commit would be added to the master branch, not the sidebar branch. We've already seen this in the demo, but to switch between branches, we need to use Git's checkout command.

```bash
git checkout sidebar
```

It's important to understand how this command works. Running this command will:

- remove all files and directories from the Working Directory that Git is tracking (files that Git tracks are stored in the repository, so nothing is lost)
- go into the repository and pull out all of the files and directories of the commit that the branch points to

### Branches In The Log

The branch information in the command prompt is helpful, but the clearest way to see it is by looking at the output of git log. But just like we had to use the --decorate flag to display Git tags, we need it to display branches.

```bash
git log --oneline --decorate
```

### Delete A Branch

A branch is used to do development or make a fix to the project that won't affect the project (since the changes are made on a branch). Once you make the change on the branch, you can combine that branch into the master branch (this "combining of branches" is called "merging" and we'll look at it shortly).

Now after a branch's changes have been merged, you probably won't need the branch anymore. If you want to delete the branch, you'd use the -d flag. The command below includes the -d flag which tells Git to delete the provided branch (in this case, the "sidebar" branch).

```bash
git branch -d sidebar
```

One thing to note is that you can't delete a branch that you're currently on. So to delete the sidebar branch, you'd have to switch to either the master branch or create and switch to a new branch.

Deleting something can be quite nerve-wracking. Don't worry, though. Git won't let you delete a branch if it has commits on it that aren't on any other branch (meaning the commits are unique to the branch that's about to be deleted). If you created the sidebar branch, added commits to it, and then tried to delete it with the git branch -d sidebar, Git wouldn't let you delete the branch because you can't delete a branch that you're currently on. If you switched to the master branch and tried to delete the sidebar branch, Git also wouldn't let you do that because those new commits on the sidebar branch would be lost! To force deletion, you need to use a capital D flag - git branch -D sidebar.

### Git Branch Recap

To recap, the git branch command is used to manage branches in Git:

```bash
# to list all branches
git branch

# to create a new "footer-fix" branch
git branch footer-fix

# to delete the "footer-fix" branch
git branch -d footer-fix
```

## Branching Effectively

First, make sure we're on the same page and have the same starter code. We're going to be working in the new-git-project project. The project has the following files:

- index.html
- css/app.css (empty)
- js/app.js (empty)

The CSS and JavaScript files are empty. Make sure the index file has the following content:

```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <title>Blog Project</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <meta name="description" content="">
    <link rel="stylesheet" href="css/app.css">
</head>
<body>

    <header>
        <h1>Expedition</h1>
    </header>

    <div class="container">
        <main>

        </main>
    </div>

    <footer>
        Made with ♥ @ Git Practice
    </footer>
    <script src="js/app.js"></script>
</body>
</html>
```

### The Game Plan

Right now we have all of our code on the master branch (which is the default branch). We're about to work with branches, by:

- adding content to them
- creating new branches
- switching back and forth between them

Let's use branches to make the following changes:

1. on the master branch - add a default color to the page
2. create a sidebar branch - create a sidebar for the page
3. on the master branch - change the heading of the page
4. on the sidebar branch - add more content to the sidebar
5. create a footer branch - add social links to the footer

### Change 1 - Add Page Color

Make sure you're on the master branch and add the following content to css/app.css:

```css
body {
    background-color: #00cae4;
}
```

Save the file. Then add the file to the staging index and commit it to the repository.

### Change 2 - Add Sidebar

Let's add a sidebar to the page. But let's say that we're not really sure if we like the new background color. So we'll place the sidebar branch on the commit before the one that sets the page's color. Your SHAs will be different, but, for me, the commit that's before the one that adds the color has a SHA of 5bfe5e7. So adding the branch to that commit would look like:

```bash
git branch sidebar 5bfe5e7
```

Now use the git checkout command to switch to the new sidebar branch.
Running a git log --oneline --decorate shows sidebar.

Did you notice that the master branch does not display in the output? Where did it go!?! Is it lost? Don't worry, it's still there, we'll see how to get it to display in just a second.

But first, in your code editor, switch to the app.css file. Notice that it does not have the CSS we previously entered! Because of this, if you load the project up in the browser, the page won't have a colored background. This makes sense since the CSS file is empty, but do you know why?

Create a sidebar by adding the following <aside> code to the HTML file:

```html
<div class="container">
    <main>

    </main>
</div>

<!-- start of new content -->
<aside>
    <h2>About Me</h2>

    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Eos, debitis earum molestias veniam suscipit aliquam totam exercitationem tempore neque vitae. Minima, corporis pariatur facere at quo porro beatae similique! Odit.</p>
</aside>
<!-- end of new content -->

<footer>
    Made with ♥ @ Git Practice
</footer>
```
I added my <aside> content next to the <main> element as a fellow child of the <div class="container"> element.

Feel free to add any content inside the <aside> element!

Don't Change the CSS

We'll change it later, but if you make a change right now, we'll end up having what's known as a "merge conflict". We'll manually cause a merge conflict in a bit, but we don't want to have one right now, so just don't make any changes to the CSS file, yet.

### Change 3 - Change Heading On Master

Let's switch back to the master branch and update the page heading.

Use the git checkout command to switch back to the master branch. (Notice that the HTML for the new sidebar is no longer there(!) because all that code is stored safely on the sidebar branch.)

Now change the `<h1>` heading of the page from "Expedition" to something else. How about something exciting like the word "Adventure"!?!

How do you have Git show you the changes you've saved, but not yet committed?

```bash
git diff
```

Now it's time to save the index.html file and make a commit to add this change to the repository. (I used the commit message "Improve site heading for SEO", but see if you can think of a better one)

### Change 4 - Add More Content To Sidebar

Switch back to the sidebar branch (notice, again, that content we've added to the master branch isn't visible on the sidebar branch).

Now just add some content inside the <aside> element. Add something about yourself - your favorite movie or book (my favorite is LOTR!). Anything will work, you just need to add some content.

Again, make sure that you do not make changes to the CSS file.

Now save the index.html file and make a commit.

### Change 5 - Add Social Links To Footer

We've made a number of changes, and we're about to make our last one. Let's add some social icons to the page's footer. For grins and giggles, let's make this change on a new footer branch that's based off the master branch. So we need to create a new footer branch, first.

Switch and Create Branch In One Command

The way we currently work with branches is to create a branch with the git branch command and then switch to that newly created branch with the git checkout command.

But did you know that the git checkout command can actually create a new branch, too? If you provide the -b flag, you can create a branch and switch to it all in one command.

```bash
git checkout -b richards-branch-for-awesome-changes
```

Let's use this new feature of the git checkout command to create our new footer branch and have this footer branch start at the same location as the master branch:

```bash
git checkout -b footer master
```

Add Social Links

Now that we're on a new branch, let's add some social links to the page's footer:



```html
<footer>
    <!-- start of new content -->
    <section>
        <h3 class="visuallyhidden">Social Links</h3>
        <a class="social-link" href="https://twitter.com/udacity">
            <img src="img/social-twitter.png" alt="Twitter">
        </a>
        <a class="social-link" href="https://www.instagram.com/udacity/">
            <img src="img/social-instagram.png" alt="Instagram">
        </a>
        <a class="social-link" href="https://plus.google.com/+Udacity">
            <img src="img/social-google.png" alt="Google Plus">
        </a>
    </section>
    <!-- end of new content -->
</footer>
```

### See All Branches At Once

We've made it to the end of all the changes we needed to make! Awesome job!

Now we have multiple sets of changes on three different branches. We can't see other branches unless in the `git log` output unless we switch to a branch. Wouldn't it be nice if we could see all branches at once in the `git log` output.

As you've hopefully learned by now, the `git log` command is pretty powerful and can show us this information. We'll use the new `--graph` and `--all` flags:

```bash
git log --oneline --decorate --graph --all
```

The `--graph` flag adds the bullets and lines to the leftmost part of the output. This shows the actual branching that's happening. The `--all` flag is what displays all of the branches in the repository.

Running this command will show all branches and commits in the repository:

### Merging

Remember that the purpose of a topic branch (like sidebar) is that it lets you make changes that do not affect the master branch. Once you make changes on the topic branch, you can either decide that you don't like the changes on the branch and you can just delete that branch, or you can decide that you want to keep the changes on the topic branch and combine those changes in with those on another branch.

Combining branches together is called merging.

Git can automatically merge the changes on different branches together. This branching and merging ability is what makes Git incredibly powerful! You can make small or extensive changes on branches, and then just use Git to combine those changes together.

It's very important to know which branch you're on when you're about to merge branches together. Remember that making a merge makes a commit.

As of right now, we do not know how to undo changes. but if you make a merge on the wrong branch, use this command to undo the merge:

```bash
git reset --hard HEAD^
(Make sure to include the ^ character! It's a known as a "Relative Commit Reference" and indicates "the parent commit".)
```

### The Merge Command

The git merge command is used to combine Git branches:

```bash
git merge <name-of-branch-to-merge-in>
```

When a merge happens, Git will:

- look at the branches that it's going to merge
- look back along the branch's history to find a single commit that both branches have in their commit history
- combine the lines of code that were changed on the separate branches together
- makes a commit to record the merge

### Fast-forward Merge

In our project, I've checked out the master branch and I want it to have the changes that are on the footer branch. If I wanted to verbalize this, I could say this is - "I want to merge in the footer branch". That "merge in" is important; when a merge is performed, the other branch's changes are brought into the branch that's currently checked out.

Let me stress that again - When we merge, we're merging some other branch into the current (checked-out) branch. We're not merging two branches into a new branch. We're not merging the current branch into the other branch.

Now, since footer is directly ahead of master, this merge is one of the easiest merges to do. Merging footer into master will cause a Fast-forward merge. A Fast-forward merge will just move the currently checked out branch forward until it points to the same commit that the other branch (in this case, footer) is pointing to.

To merge in the footer branch, run:

```bash
git merge footer
```

### Perform A Regular Merge

Let's do the more common kind of merge where two divergent branches are combined. You'll be surprised that to merge in a divergent branch like sidebar is actually no different!

To merge in the sidebar branch, make sure you're on the master branch and run:

```bash
git merge sidebar
```

Because this combines two divergent branches, a commit is going to be made. And when a commit is made, a commit message needs to be supplied. Since this is a merge commit a default message is already supplied. You can change the message if you want, but it's common practice to use the default merge commit message. So when your code editor opens with the message, just close it again and accept that commit message.

The merges we just did were able to merge successfully. Git is able to intelligently combine lots of work on different branches. However, there are times when it can't combine branches together. When a merge is performed and fails, that is called a merge conflict.

### Merge Conflicts

Sometimes Merges Fail
Most of the time Git will be able to merge branches together without any problem. However, there are instances when a merge cannot be fully performed automatically. When a merge fails, it's called a merge conflict.

If a merge conflict does occur, Git will try to combine as much as it can, but then it will leave special markers (e.g. >>> and <<<) that tell you where you (yep, you the programmer!) needs to manually fix.

What Causes A Merge Conflict

As you've learned, Git tracks lines in files. A merge conflict will happen when the exact same line(s) are changed in separate branches. For example, if you're on a alternate-sidebar-style branch and change the sidebar's heading to "About Me" but then on a different branch and change the sidebar's heading to "Information About Me", which heading should Git choose? You've changed the heading on both branches, so there's no way Git will know which one you actually want to keep. And it sure isn't going to just randomly pick for you!

Let's force a merge conflict so we can learn to resolve it. Trust me, it's simple once you get the hang of it! Remember that a merge conflict occurs when Git isn't sure which line(s) you want to use from the branches that are being merged. So we need to edit the same line on two different branches...and then try to merge them.

Forcing A Merge Conflict!

Remember that a merge conflict occurs when the exact same line(s) are changed in separate branches. Let's alter the page's heading on two different branches. So Let's:

- change the heading on the master branch
- create a heading-update branch that's located on the commit right before the recently modified master branch
- change the same heading
- switch back to the master branch
- merge in the heading-update branch

Change Heading On Branch 1
Since the master branch is just a regular ol' branch like all the rest, let's just alter the heading while we're on the master branch. So change the `<h1>` heading from whatever you have it to something else. For me, the heading is currently "Adventure" on line 13, and I'm changing it to "Quest".

Once you've made the change, save the file and commit it to the repository.

Change Heading On Branch 2
Now we need to create a different branch and update the heading on that branch.

Now this is important, we need to create a branch that's not branching from the master branch. If we make a change that branches off of the master branch, then that change will be "ahead" of this one and Git will just use that change instead of the one we just made on master. So we need to put the branch "in the past".

Let's just create a branch that's on the commit right before the most recent one. So use Git log to get the previous commit's SHA and create a branch on that commit.

Ok, now that we've got our branch created, we just need to update the heading, again. Now make sure you change the exact same line that you changed on the master branch. I'm changing "Adventure" on line 13 to "Crusade".

Then save the file and commit it to the repository.

Make sure you're on the master branch (we could really do this on either branch, but I just have a habit of keeping the master branch the main one that other topic branches get merged into) and merge in the heading-update branch:

```bash
git merge heading-update
```

Notice that right after the git merge heading-update command, it tries merging the file that was changed on both branches (index.html), but that there was a conflict. Also, notice that it tells you what happened - "Automatic merge failed; fix conflicts and then commit the result".

Remember our good friend git status? Well he'll come in really handy when working with merge conflicts.

The git status output tells us to that the merge conflict is inside index.html. So check out that file in your code editor!

Resolving A Merge Conflict
Git is using the merge conflict indicators to show you what lines caused the merge conflict on the two different branches as well as what the original line used to have. So to resolve a merge conflict, you need to:

choose which line(s) to keep
remove all lines with indicators

## Undoing Changes

### Modifying The Last Commit

You've already made plenty of commits with the git commit command. Now with the --amend flag, you can alter the most-recent commit.

If your Working Directory is clean (meaning there aren't any uncommitted changes in the repository), then running git commit --amend will let you provide a new commit message. Your code editor will open up and display the original commit message. Just fix a misspelling or completely reword it! Then save it and close the editor to lock in the new commit message.

Add Forgotten Files To Commit

Alternatively, `git commit --amend` will let you include files (or changes to files) you might've forgotten to include. Let's say you've updated the color of all navigation links across your entire website. You committed that change and thought you were done. But then you discovered that a special nav link buried deep on a page doesn't have the new color. You could just make a new commit that updates the color for that one link, but that would have two back-to-back commits that do practically the exact same thing (change link colors).

Instead, you can amend the last commit (the one that updated the color of all of the other links) to include this forgotten one. To do get the forgotten link included, just:

- edit the file(s)
- save the file(s)
- stage the file(s)
- and run `git commit --amend`

So you'd make changes to the necessary CSS and/or HTML files to get the forgotten link styled correctly, then you'd save all of the files that were modified, then you'd use `git add` to stage all of the modified files (just as if you were going to make a new commit!), but then you'd run `git commit --amend` to update the most-recent commit instead of creating a new one.

### Reverting A Commit

When you tell Git to revert a specific commit, Git takes the changes that were made in commit and does the exact opposite of them. Let's break that down a bit. If a character is added in commit A, if Git reverts commit A, then Git will make a new commit where that character is deleted. It also works the other way where if a character/line is removed, then reverting that commit will add that content back!

We ended the previous lesson with a merge conflict and resolved that conflict by setting the heading to Adventurous Quest. Let's say that there's a commit in your repository that changes the heading now to Quests & Crusades.

Now that I've made a commit with some changes, I can revert it with the git revert command

```bash
git revert <SHA-of-commit-to-revert>
```

Since the SHA of the most-recent commit is `db7e87a`, to revert it: I'll just run `git revert db7e87a` (this will pop open my code editor to edit/accept the provided commit message)

### Resetting Commits

At first glance, resetting might seem coincidentally close to reverting, but they are actually quite different. Reverting creates a new commit that reverts or undos a previous commit. Resetting, on the other hand, erases commits!

You've got to be careful with Git's resetting capabilities. This is one of the few commands that lets you erase commits from the repository. If a commit is no longer in the repository, then its content is gone.

To alleviate the stress a bit, Git does keep track of everything for about 30 days before it completely erases anything. To access this content, you'll need to use the `git reflog` command.

## Working With Remotes

### Add A Remote Repository

The git remote command will let you manage and interact with remote repositories.

```bash
git remote
```

If you haven't configured a remote repository then this command will display nothing. One caveat to this is if you have cloned a repository. If you have, then your repository will automatically have a remote because it was cloned from the repository at the URL you provided. Let's look at a repository that has been cloned.

The output of git remote is just the word origin. Well that's weird. The word "origin", here, is referred to as a "shortname". A shortname is just a short and easy way to refer to the location of the remote repository. A shortname is local to the current repository (as in, your local repository). The word "origin" is the defacto name that's used to refer to the main remote repository. It's possible to rename this to something else, but typically it's left as "origin".

If you want to see the full path to the remote repository, then all you have to do is use the -v (verbose) flag.

### Create A Simple Project

We're going to need a sample project to test out working with remote repositories, sending updates to the remote repository, and getting changes from the remote repository, too.

- create a new directory for your project with the name `my-travel-plans`
- use `git init` to turn the `my-travel-plans` directory into a Git reposity
- create a `README.md` file
- create `index.html`
- create `app.css`

README File Content

```markdown
# Travel Destinations

A simple app to keep track of destinations I'd like to visit.
```

HTML File Content
Add the following content to the index.html file:

```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <title>Travels</title>
    <meta name="description" content="">
    <link rel="stylesheet" href="css/app.css">
</head>
<body>

    <div class="container">
        <div class="destination-container">
            <div class="destination" id="florida">
                <h2>Florida</h2>
            </div>

            <div class="destination" id="paris">
                <h2>Paris</h2>
            </div>
        </div>
    </div>

</body>
</html>
```

CSS File Content
Add the following information to the CSS file:

```css
html {
    box-sizing: border-box;
    height: 100%;
}

*,
*::before,
*::after {
    box-sizing: inherit;
}

body {
    display: flex;
    margin: 0;
    height: 100%;
}

.container {
    margin: auto;
    padding: 1em;
    width: 80%;
}

.destination-container {
    display: flex;
    flex-flow: wrap;
    justify-content: center;
}

.destination {
    background: #03a9f4;
    box-shadow: 0 1px 9px 0 rgba(0, 0, 0, 0.4);
    color: white;
    margin: 0.5em;
    min-height: 200px;
    flex: 0 1 200px;
    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;
}

h2 {
    margin: 0;
    transform: rotate(-45deg);
    text-shadow: 0 0 5px #01579b;
}

#florida {
    background-color: #03a9f4;
}

#paris {
    background-color: #d32f2f;
}
```

Make sure to turn the project into a Git repo and committed the file with git commit.

Now create a new repository on GitHub and typically you want to use the name of your project as the name of the repository. Creating a repository, modifying it later, or deleting it is relatively easy so don't feel like you have to get the name perfect right here on this page. I'm going to create a repository called "my-travel-plans" that's the same name as the sample project I created.

I'm also going to leave the "Initialize this repository with the README" option unchecked because I don't want GitHub to add a README file for me.

Make sure that you leave the "Initialize this repository with the README" unchecked. We'll be providing our own README, so we don't want GitHub to provide one automatically.

Also, if we let GitHub auto-generate a new README file for us, then we won't be provided with the setup commands to run in the terminal. It's still possible to get that information, but it will be hidden away.

So just make sure to leave this field unchecked, and you'll be good to go!

Now just click that big "Create Repository" button to create your remote repository!

Remember that the git remote command is used to create and manage remote repositories.

There are a couple of things to notice about the command you just ran on the command line:

1. first, this command has the sub command add
2. the word origin is used - this is setting the shortname that we discussed earlier: Remember that the word origin here isn't special in any way. If you want to change this to repo-on-GitHub, then (before running the command) just change the word "origin" to "repo-on-GitHub": `$ git remote add repo-on-GitHub https://github.com/lzyacht/my-travel-plans.git`
3. third, the full path to the repository is added (i.e. the URL to the remote repository on the web)

Now use `git remote -v` to verify that you've added the remote repository correctly.

Recap

A remote repository is a repository that's just like the one you're using but it's just stored at a different location. To manage a remote repository, use the `git remote` command.

- It's possible to have links to multiple different remote repositories.
- A shortname is the name that's used to refer to a remote repository's location. Typically the location is a URL, but it could be a file path on the same computer.
- `git remote add` is used to add a connection to a new remote repository.
- `git remote -v` is used to see the details about a connection to a remote.

### Push Changes To A Remote

I used the following log command to display these commits

```bash
git log --oneline --graph --decorate --all
```

These commits are only in the local repository, though. They haven't been sent up to the remote repository yet. When commits are sent to the remote a remote branch indicator will appear in the log. Since there aren't any remote branch indicators we can tell that there are no commits on the remote repository. But just to be 100% certain let's look at the remote repository on GitHub to see if there any commits.

Since we haven't sent any commits update to GitHub yet it's still showing us the setup screen to tell us how we can connect our local repository to the remote repository and send some commits. Since this is still the setup screen we can know that there are no commits in the remote repository.

To send local commits to a remote repository you need to use the `git push` command. You provide the remote short name and then you supply the name of the branch that contains the commits you want to push:

```bash
git push <remote-shortname> <branch>
```

My remote's shortname is `origin` and the commits that I want to push are on the `master` branch. So I'll use the following command to send my commits to the remote repository on GitHub:

```bash
git push origin master
```

There a couple of things to notice:

- Depending on how you have configured GitHub and the remote URL that's being used, you might have to enter your username and password. (This will happen if you use the HTTP version of the remote rather than the ssh version.)
- If you have to enter your username and password your username will show up after typing but your password will not. So just keep typing your password and press enter when you're done.

Now before we move on, let's just check the local repository to see how it changed after pushing.

```bash
git log --oneline --graph --decorate --all
```

We now have a new marker in the output! This marker is `origin/master` and is called a tracking branch. A tracking branch's name includes the shortname of the remote repository as well as the name of the branch. So the tracking branch `origin/master` is telling us that the remote origin has a master branch that points to commit 9b7d28f (and includes all of the commits before 9b7d28f). This is really helpful because this means we can track the information of the remote Repository right here in our local one!

One very important thing to know is that this `origin/master` tracking branch is not a live representation of where the branch exists on the remote repository. If a change is made to the remote repository not by us but by someone else, the origin/master tracking branch in our local repository will not move. We have to tell it to go check for any updates and then it will move.

Recap
The `git push` command is used to send commits from a local repository to a remote repository.

```bash
git push origin master
```

The `git push` command takes:

- the shortname of the remote repository you want to send commits to
- the name of the branch that has the commits you want to send

### Pulling Changes From A Remote

Let’s say that we are in a situation where there are commits on the remote repository that we do not have in our local repository. This can happen in several ways: You could be working on a team, and a co-worker has pushed new changes to the remote. Alternatively, you could be working on the same project but from different computers -- for example, say you have a work computer and a personal computer, and you contribute to the repo from both of them. If you push changes to the repo from your work computer, the local repo on your personal computer will not reflect those changes. How do we sync new changes that are on the remote into the local repository? That's exactly where we're going to be looking at now. Let's first look at how pulling in remote changes works in theory, then we'll actually do it ourselves!

Since we don't have any commits on our remote repository yet and we're not collaborating with anybody we're going to fake it and add some commits manually through GitHub's interface on the web.

Add the following new ruleset to app.css:

```css
.destination:hover h2 {
    transform: rotate(0deg);
}
```

Add `transition: transform 0.5s`; to the `h2` ruleset, so it should now be:

```css
h2 {
    margin: 0;
    transform: rotate(-45deg);
    transition: transform 0.5s;
    text-shadow: 0 0 5px #01579b;
}
```

Because GitHub has a web interface, it allows you to add commits manually through its interface. But just because you can do a thing, doesn't mean you should. I've demoed making these changes this way so that we could simulate commits being on the remote repository but not in the local repository. But I recommend that you should always work locally on a project and then push those changes to the remote repository.

Now let's compare our local repository and our remote repository. We only have three commits in our local repository.

While there are actually four commits in the remote repository.

The local commits end at commit 5a010d1 while the remote has two extra commits - commit 4b81b2a and commit b847434.

Also, notice that in our local repository when we did the git log the origin/master branch is still pointing to commit 5a010d1.

Remember that the origin/master branch is not a live mapping of where the remote's master branch is located. If the remote's master moves, the local origin/master branch stays the same. To update this branch, we need to sync the two together.

git push will sync the remote repository with the local repository. To do the opposite (to sync the local with the remote), we need to use git pull. The format for git pull is very similar to git push - you provided the shortname for the remote repository and then the name of the branch you want to pull in the commits.

```bash
git pull origin master
```

There's several things to note about running this command:

- the format is very similar to that of git push - there's counting and compressing and packing of items
- it has the phrase "fast-forward" which means Git did a fast-forward merge (we'll dig into this in just a second)
- it displays information similar to git log --stat where it shows the files that have been changed and how many lines were added or removed in them

If you don't want to automatically merge the local branch with the tracking branch then you wouldn't use git pull you would use a different command called git fetch. You might want to do this if there are commits on the repository that you don't have but there are also commits on the local repository that the remote one doesn't have either.

Recap

If there are changes in a remote repository that you'd like to include in your local repository, then you want to pull in those changes. To do that with Git, you'd use the git pull command. You tell Git the shortname of the remote you want to get the changes from and then the branch that has the changes you want:

```bash
git pull origin master
```

When git pull is run, the following things happen:

- the commit(s) on the remote branch are copied to the local repository
- the local tracking branch (origin/master) is moved to point to the most recent commit
- the local tracking branch (origin/master) is merged into the local branch (master)

### Pull vs Fetch

Git fetch is used to retrieve commits from a remote repository's branch but it does not automatically merge the local branch with the remote tracking branch after those commits have been received.

You provide the exact same information to git fetch as you do for git pull. So you provide the shortname of the remote repository you want to fetch from and then the branch you want to fetch:

```bash
git fetch origin master
```

When git fetch is run, the following things happen:

- the commit(s) on the remote branch are copied to the local repository
- the local tracking branch (e.g. origin/master) is moved to point to the most recent commit

The important thing to note is that the local branch does not change at all.

You can think of git fetch as half of a git pull. The other half of git pull is the merging aspect.

One main point when you want to use git fetch rather than git pull is if your remote branch and your local branch both have changes that neither of the other ones has. In this case, you want to fetch the remote changes to get them in your local branch and then perform a merge manually. Then you can push that new merge commit back to the remote.

Recap
You can think of the git pull command as doing two things:

1. fetching remote changes (which adds the commits to the local repository and moves the tracking branch to point to them)
2. merging the local branch with the tracking branch

The git fetch command is just the first step. It just retrieves the commits and moves the tracking branch. It does not merge the local branch with the tracking branch. The same information provided to git pull is passed to git fetch:

- the shorname of the remote repository
- the branch with commits to retrieve

```bash
git fetch origin master
```

## Working On Another Developer's Repository

### Forking A Repository

In version control terminology if you "fork" a repository that means you duplicate it. Typically you fork a repository that belongs to someone else. So you make an identical copy of their repository and that duplicate copy now belongs to you.

This concept of "forking" is also different from "cloning". When you clone a repository, you get an identical copy of the repository. But cloning happens on your local machine and you clone a remote repository. When you fork a repository, a new duplicate copy of the remote repository is created. This new copy is also a remote repository, but it now belongs to you.

## Staying In Sync With A Remote Repository

### Create a Pull Request

A pull request is a request to the original or source repository's maintainer to include changes in their project that you made in your fork of their project. You are requesting that they pull in changes you've made.

To create a pull request, a couple of things need to happen:

- you must fork the source repository
- clone your fork down to your machine
- make some commits (ideally on a topic branch!)
- push the commits back to your fork
- create a new pull request and choose the branch that has your new commits

### Stay in sync with source project

Stars & Watching
If you want to keep up-to-date with the Repository, GitHub offers a convenient way to keep track of repositories - it lets you star repositories:

You can go to `https://github.com/stars` to list out and filter all of the repositories that you have starred.
