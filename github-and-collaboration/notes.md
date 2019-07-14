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

## Sending Commits
To send local commits to a remote repository, you need to use the `git push` command. You provide the remote short name and then you supply the name of the branch that contains the commits you want to push:

    $ git push <remote-shortname> <branch>