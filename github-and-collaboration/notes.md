# Github and Collaboration

## Always Use Topic Branches

Remember that it's incredibly helpful to make all your commits on descriptively named **topic branhces**. Branches help isolate unrelated changes from each other. So when you are collaborating with other developers, make sure to create a new branch that has a descriptive name that describes what changes it contains.

       $ git remote

The `git remote` command will let you manage and interact with remote repositories. If you have cloned a repository, your repository will automatically have a remote because it was cloned from the repository at the URL you provided.

## Remote Shortnames

the output of `git remote` is just the word `origin`. The word 'origin' here is referref to as a shortname. A shortname is just a short and easy way to refer to the location of the remote repository. A shortname is local to the current repository. The word 'origin' is the defacto name that's used to refer to the main remote repository. It is posible to rename this to something else, but typically its left as 'origin'.

If you want to see the full path of the remote respository, then all you have to do is use the `-v` flag

        $ git remote -v

To add a remote branch, use

    git remote add origin https://github.com/wechuli/my-travel-plans.git

There are a couple of things to notice about the command run above

1. first, this command has the sub command `add`
2. the word `origin` is used - this is setting the shortname
   - Remember that the word `origin` here isn't special in any way, you can change it to whatever you like
3. third, the full path to the respository is added(i.e the URL to the remote repository on the web)

We can remove a remote branch using

    git remote remove {name_of_branch}

It is possible to have links to multiple different remote repositories.

## Git log

The `git log` command displays all of the commits in a repository's history. By default, the command displays each commit's:

- Secure Hash Algorithm(SHA)
- author
- date
- commit message

  \$ git log --oneline --graph --decorate --all

## Sending Commits

To send local commits to a remote repository, you need to use the `git push` command. You provide the remote short name and then you supply the name of the branch that contains the commits you want to push:

    $ git push <remote-shortname> <branch>

This marker is `origin/master` and is called a **tracking branch**. A tracking branch's name includes the shortname of the remote repository as well as the name of the branch. so the tracking branch `origin/master` is telling us that the remote `origin` has a branch that points to commit \_\_. This is really helpful because this means we can track the information of the remote Repository right in our local one.

One very important thing to know is that this `origin/master` tracking branch is not a live representation of where the branch exists on the remote repository. If a change is made to the remote repository by someone else, the `origin/master` tracking branch in our local repository will not move. We have to tell it to go check for any updates and then it will move.

## Pull changes from a remote

Let's say that we are in a situation where there are commits on the remote repository that we do not have in our local repository.

        $git pull origin master

The branch that appears in the _local_ repository is actually tracking a branch in the remote repository(e.g `origin/master` in the local repository is a tracking branch because it's tracking the progress of the `master` branch on the remote repository that has the shortname "origin")

Remember that the `origin/master` branch is not a live mapping of where the remote's master branch is located. If the remote's `master` moves, the local `origin/master` branch stays the same. To update this branch, we need to sync the two together.

`git push` will sync the remote repository with the local repository. To do the opposit(to sync the local with the remote), we need to use `git pull`.

If you don't want to automatically merge the local branch with the tracking branch then you wouldn't use `git pull`, you would use a different command `git fetch`. You might want to do this if there are commits on the respository that you don't have but there are also commits on the local respository that the remote one doesn't have either.

When `git pull` is run, the following things happen

- the commits(s) on the remote branch are copied to the local repository
- the local tracking branch(`origin/master`) is moved to point to the most recent commit
- the local tracking branch(`origin/master`) is merged into the local branch(`master`)

Git fetch is used to retrieve commits from a remote respository's branch but it does not automatically merge the local branch with the remote tracking branch after those commits have been received.

You provide the exact same information to `git fetch` as you do for `git pull`. So you provide the shortname of the remote repository you want to fetch from and then the branch you want to fetch

        $git fetch origin master

When `git fetch` is run, the follwowing things happen:

- the commit(s) on the remote branch are copied to the local repository
- the local tracking branch(e.g `origin/master` is moved to point to the most recent commit)

The important thing to note is that the local branch does not change at all.

One main point when you want to use git fetch rather than git pull is if your remote branch and your local branch both have changes that neither of the other ones has. In this case, you want to fetch the remote changes to get them in your local branch and then perform a merge manually. Then you can push that new merge commit back to the remote.

## Forking

In version control terminology if you "fork" a repository, that means you duplicate it. Typically you fork a repository that belongs to someone else. So you make an identical copy of their repository and that duplicate copy now belongs to you.

This concept of "forking" is also different from "cloning". When you clone a repository, you get an identical copy of the repository. But cloning happens on your local machine and you clone a remote repository. When you fork a repository, a new duplicate copy of the remote repository is created. This new copy is also a remote repository, but it now belongs to you.

Forking is not done on the command line; there is no `git fork` command.

If you fork the repository to your own account then you will have full control over that repository. Because forking a repository gives you a copy of it in your account, you can clone down to your computer, make changes to it, and then push those changes back to the forked repository. But you need to keep in mind that it'll be pushing the changes back to your remote repository not to the original repository that you forked from.

### git diff

Shows file differences not yet staged.

### `git push [alias] [branch]`

Uploads all local branch commits to GitHub.

Forking is an action that's done on a hosting service, like GitHub. Forking a repository creates an identical copy of the original repository and moves this copy to your account. You have total control over this forked repository. Modifying your forked repository does not alter the original repository in any way.

## Reviewing Existing Work

When you're the sole developer on a project, it's easy to know what progress has been doen on the project because you did everything yourself. Things can become a bit more complicated, though, when you're working on a team - whether that team is local in an office or if you are developing with someone just across the internet.

Sometimes it can be hard to see what the other developers have been doing on the project, especially if the developers are working across multiple different branches.

We can discover details about what other developers have done by using the extremely powerful `git log` command.

### Filtering Collaborator's Commits

Being able to narrow down the commits to just the ones you're looking for can be a chore. There are different ways we can discover information that our collaboratos have done!

#### Group By Commit Author

A quick way that we can see how many commits each contributor has added to the repository is to use the `git shortlog` command:

    $ git shortlog

`git shortlog` displays an alphabetical list of names and commit messages that go along with them. If we just want to see the number of commits that each developer has made, we can add a couple of flags `-s` to show just the number of commits(rather than each commit's message) and `-n` to sort them numerically(rather than alphabetically by author name)

        $ git shortlog -s -n

### Filter By Author

Another way that we can display all of the commits by an author is to use the regular `git log` command but include the `--author` flag to filter the commits to the provided author.

        $git log --author=Surma



        git show {commit SHA}

### Filter Commits By Search

It is important to write good, descriptive commit messages.If you write a descriptive commit message, then it's so much easier to search through the commit messages later, to find exactly what you're looking for.

And remeber, if the commit message is not enough for you to explain what the commit is for, you can provide a detailed description of exactly why the commit is needed in the description area.

We can filter commits with the `--grep` flag.

How about we filter down to just the commits that reference the word "bug". We can do that with either of the following commands:

    $git log --grep=bug
    $git log --grep bug
    $git log --grep "unit tests"

### Summary

The `git log` command is extremely powerful and you can use it to discover a lot about a repository. But it can be especially helpful to discover information about a repository that you're collaborating on with others.

You can use `git log` to:

- group commits bu author with `git shortlog`
  \$git shortlog
- filter commits with the `--author` flag
  \$git log --author="Richard Kalehoff"
- filter commits using the `--grep` flag
  \$git log -grep="border radius issue in Safari"

## Determing What To Work On

If you have forked a project and you have code in your fork that's not in the original project, you can get code into the original project by sending the original project's maintainer a request to include your code changes. This request is known as a "Pull Request"

### How to Contribute

- The first thing you should always look for in a project is a file with the name CONTIBUTING.md. This file lists out the information you should follow to contribute to the project. You should look for this file before you start doing development work of any kind.

### GitHub Issues

If your code change is a simple spelling mistake then you can probably just fo ahead and make that change. But if your change is more substantial where it modifies a number of files in a significant way, you probably want to get approval by the project's maintainer(s) before you start working on it.

GitHub has a fantastic interface for asking questions of the project maintainer in an open way that lets everyone see what's being done with the project. This is the GitHub Issues interface.

Now, "issues" doesn't mean that there's actually a bug, it can just be any change that needs to be made to the project. GitHub's issue tracker is quite sophisticated. Each issue can:

- have a label or multiple labels applied to it
- can be assigned to an individual
- can be assigned to a milestone (for example the issue will be resolved by the next major release)

But probably one of the most important aspects of the issue tracker is that each issue can have its own comments, so a conversation can form around the issue.

Another thing that's nice about issues is:

- they let you subscribe to an issue so you'll be notified of new comments and code changes
- you can communicate back and forth with a project maintainer on a specific change.

Before you contribute anything to a file, check out the instructions in CONTRIBUTING.md . Then check out the project's issues and look to see if there's anything that's similar to what you want to contribute. If there is, then subscribe to that issue and read the existing conversation to see if you can help.

If you've looked through the list of issues and don't see one that is similar to what you want to do, then you can create a new issue of your own. On every page of the GitHub issues interface, you'll find the new issue button

### New Issue Page

One really cool thing about the new issue page is that, if the project has a CONTRIBUTING.md file, it will display a notification at the top of the page recommending that you check out the guidelines on how to contribute to the project. Clicking on the "guidelines for contributing" link takes you to the CONTRIBUTING.md file.

The GitHub issues interface support markdown so when you create your issue you can use Markdown to format it and exactly the way you want by including links, images, bulleted lists, and code blocks.

Just like crafting a descriptive commit message, you want to create an issue with an informative title that explains briefly what you want to do. Then, in the comments section, provide plenty of detail on what the change is, or why you think it's needed, or how this will make the project better.

Typically, the project's maintainer has a full-time job and works on their project on the side, so give them some time to respond to your issue before you dive in and start making your changes. Once the project maintainer has given you the go-ahead it's time to start working on the changes you want to contribute back to the project.

### Topic Branches

The best way to organize the set of commits/changes you want to contribute back to the project is to put them all on a topic branch.
Unlike the master branch which is the default branch that holds all of the commits for your entire project, a topic branch host commits for just a single concept or single area of change.

For example if there is a problem with the login form for logging into the website, then a branch name to address this specific issue could be called:

- login
- login-bug
- signup-bug
- login-form-bug etc.

There are plenty of names that can be used for a topic branch's name. You just want to use a clear descriptive name for the branch so that if, for example, you list out all of the branches you can immediately see what changes are supposed to be in a branch just by its name.

One thing to keep in mind is that sometimes a project has specific requirements on what to name your topic branch. For example, if a branch is going to be addressing bug fixes, then many projects require a bugfix- prefix. Going back to our branch that was dealing with a bug with the login form, it would have to be named something like bugfix-login-form. So definitely check out the CONTRIBUTING.md file to see if they provide instructions on what you should name your topic branches.

### Best Practices

#### Write Descriptive Commit Messages

Write clear, descriptive commit messages. The more descriptive your branch name and commit messages are the more likely it is that the project's maintainer will not have to ask you questions about the purpose of your code or have dig into the code themselves. The less work the maintainer has to do, the faster they'll include your changes into the project.

#### Create Small, Focused Commits

Make sure when you are commiting changes to the project that you make smaller commits. Don't make massive commits that record 10+ file changes and changes to hundres of lines of code. You want to make smaller, more frequent commits that record just a handlful of file changes with a smaller number of line changes.

Think about it this way: if the developer does not like a portion of the changes you're adding to a massive commit, there's no way for them to say, "I like commit A, but just not the part where you change the sidebar's background color." A commit can't be broken down into smaller chunks, so make sure your commits are in small enough chunks and that each commit is focused on altering just one thing. This way the maintainer can say I like commits A, B, C, D, and F but not commit E

#### Update The ReadME

And lastly, if any code changes that you're adding drastically changes the project, you should update the ReadME file to instruct others about this change.

### Recap

Before you start doing any work, make sure to look for the project's CONTRIBUTING.md file.

Next, it's a good idea to look at the GitHub issues for the project

- look at the existing issues to see if one is similar to the change you want to contribute
- if necessary create a new issue
- communicate the changes you'd like to make to the project maintainer in the issue

When you start developing, commit all of your work on a topic branch:

- do not work on the master branch
- make sure to give the topic branch clear, descriptive name

As a general best practice for writing commits:

- make frequent, smaller commits
- use clear and descriptive commit messages
- update the README file, if necessary

## Staying in Sync With a Remote Repo

A pull request is a request to the original or source repository's maintainer to include changes in their project that you made in your fork of their project. You are requesting that they pull in changes you've made.

## Steps to follow when collaborating

- Review the projects's contributing.md file
- Check out the project's existing ideas
- talk with the project maintainer about the change

## Recap

A pull request is a request for the source repository to pull in your commits and merge them with their project. To create a pull request, a couple of things need to happen:

- you must fork the source repository
- clone your fork down to your machine
- make some commits(ideally on a topic branch)
- push the commits back to your fork
- create a new pull request and choose the branch that has your new commits

## Stay in sync with source project

While you're working on a topic branch of changes that you want to make a repository, that repository will probably be receiving updates of its own from the original authors.

### Stars & Watching

If you want to keep up-to-date with the Repository, GitHub offers a convenient way to keep track of repositories - it lets you star repositories:

You can go to https://github.com/stars to list out and filter all of the repositories that you have starred.

Starring is helpful if you want to keep track of certain repositories. But it's not entirely helpful if you need to actively keep up with a repositories development because you have to manually go to the stars page to view the repositories and see if they've changed.

### Watching a Repository

If you need to keep up with a project's changes and want to be notified of when things change, GitHub offers a "Watch" feature:

If you're working on a repository quite often, then I'd suggest setting the watch setting to "Watching". This way GitHub will notify you whenever anything happens with the repository like people pushing changes to the repository, new issues being created, or comments being added to existing issues.

### Including Upstream Changes

Now that you know about watching your repository let say that you're watching it and you get notified that some commits have been pushed to the original, source repository. How do you go about getting those changes into your fork of the repository? If you want to keep doing development on your fork then you'd need your fork to stay in sync with the source repository as much as possible.

Remember that the word origin is just the default name that's used when you git clone a remote repository for the first time. We're going to use the git remote command to add a new shortname and URL to this list. This will give us a connection to the source repository.

        git remote add upstream https://github.com/udacity/course-collaboration-travel-plans.git

Notice that I've used the name upstream as the shortname to reference the source repository. As with the origin shortname, the word upstream here is not special in any way; It's just a regular word. This could have been any word... like the word "banana". But the word "upstream" is typically used to refer to the source repository.

#### Origin vs Upstream Clarification

One thing that can be a tiny bit confusing right now is the difference between the origin and upstream. What might be confusing is that origin does not refer to the source repository (also known as the "original" repository) that we forked from. Instead, it's pointing to our forked repository. So even though it has the word origin is not actually the original repository.

Remember that the names origin and upstream are just the default or de facto names that are used. If it's clearer for you to name your origin remote mine and the upstream remote source-repo, then by all means, go ahead and rename them. What you name your remote repositories in your local repository does not affect the source repository at all.

You can rename remotes as follows

    $ git remote rename mine origin
    $ git remote rename source-repo upstream

#### Retrieving Upstream Changes

Now to get the changes from upstream remote repository, all we have to do is run `git fecth` and use the upstream shortname rather than the origin shortname

        git fetch upstream master

Now that we've fetched all of the changes from the upstream remote repository, let's do a log to see what new information we have in our local repository. I'm using the following git log command to make sure I display all commits from all branches (including remote and tracking branches!):

    $ git log --oneline --graph --decorate --all

It can be a bit difficult to read with the wrapping of the commit messages but you should be able to see that there is now an upstream/master remote branch that is ahead of the local master branch. upstream/master is on commit 52e493f while the master branch is on commit 1c12194.

We can use the upstream/master branch to keep track of where the source repository's master branch is. We can now get any changes that are made to the source repository's master branch by just running git fetch upstream master

To push these new changes from the Lam's repository, we don't want to run git push origin upstream/master because upstream/master is not a local branch. To get these changes into my forked version of her project, I could merge upstream/master into an existing branch (like the local master branch) and push that.

#### to make sure I'm on the correct branch for merging

        $ git checkout master

#### merge in Lam's changes

        $ git merge upstream/master

#### send Lam's changes to _my_ remote

        $ git push origin master

### Recap

When working with a project that you've forked. The original project's maintainer will continue adding changes to their project. You'll want to keep your fork of their project in sync with theirs so that you can include any changes they make.

To get commits from a source repository into your forked repository on GitHub you need to:

- get the cloneable URL of the source repository
- create a new remote with the git remote add command
  - use the shortname upstream to point to the source repository
  - provide the URL of the source repository
- fetch the new upstream remote
- merge the upstream's branch into a local branch
- push the newly updated local branch to your origin repo

### Manage an active PR

The project maintainer may decide not to accept your changes right away. They might request you to make some additional changes to your code before accepting your request and merging in your changes. Most likely they will communicate their desired changes through the conversation on the pull requests page.

If the project's maintainer is requesting changes to the pull request, then:

- Make any necessary commits on the same branch in your local repository that your pull request is based on.
- Push the branch to your fork of the source repository.

The commits will then show up on the pull request page.

### Squash Commits

To squash commits together, we're going to use the extremely powerful `git rebase` command. This is

#### The Rebase Command

The `git rebase` command will move commits to have a new base. In the command `git rebase -i HEAD~3` we're telling Git to use `HEAD~3` as the base where all of the other commits `HEAD~2` `HEAD~1` and `HEAD` will connect to.

The `-i` in the command stands for interactive. You can perform a rebase in a non-interactive mode.

`HEAD` indicates your current location (it could point to several things, but typically it'll either point to a branch name or directly to a commit's SHA). The ~3 part means "three before", so `HEAD~3` will be the commit that's three before the one you're currently on. We're using this relative reference to a commit in the `git rebase` command.

We need to force the push after rebasing. `git rebase` creates a new commit with a new SHA.

#### Rebase Commands

Let's take another look at the different commands that you can do with git rebase:

- use p or pick – to keep the commit as is
- use r or reword – to keep the commit's content but alter the commit message
- use e or edit – to keep the commit's content but stop before committing so that you can:
  - add new content or files
  - remove content or files
  - alter the content that was going to be committed
- use s or squash – to combine this commit's changes into the previous commit (the commit above it in the list)
- use f or fixup – to combine this commit's change into the previous one but drop the commit message
- use x or exec – to run a shell command
- use d or drop – to delete the commit

#### When to rebase

As you've seen, the git rebase command is incredibly powerful. It can help you edit commit messages, reorder commits, combine commits, etc. So it truly is a powerhouse of a tool. Now the question becomes "When should you rebase?".

Whenever you rebase commits, Git will create a new SHA for each commit! This has drastic implications. To Git, the SHA is the identifier for a commit, so a different identifier means it's a different commit, regardless if the content has changed at all.

So you should not rebase if you have already pushed the commits you want to rebase. If you're collaborating with other developers, then they might already be working with the commits you've pushed. If you then use git rebase to change things around and then force push the commits, then the other developers will now be out of sync with the remote repository. They will have to do some complicated surgery to their Git repository to get their repo back in a working state...and it might not even be possible for them to do that; they might just have to scrap all of their work and start over with your newly-rebased, force-pushed commits.

The git rebase command is used to do a great many things.

Inside the interactive list of commits, all commits start out as pick, but you can swap that out with one of the other commands (reword, edit, squash, fixup, exec, and drop).

I recommend that you create a backup branch before rebasing, so that it's easy to return to your previous state. If you're happy with the rebase, then you can just delete the backup branch!
