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
