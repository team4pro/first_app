# 501k Website

This website uses Ruby on Rails.


## Git'n started

1. Install `ruby-1.9.2` somehow.
    * If you have `rvm` (*nix):
            rvm install ruby-1.9.2
            rvm use ruby-1.9.2
            rvm gemset create levi
    
      `rvm` is not required though.

1. Install `git` somehow.

    * On the Mac, you should also install `gitx`.

1. Create a GitHub account.

1. Go to [roy98102/levi](https://github.com/roy98102/levi) and click "Fork".

1. Then:
        git clone git@github.com:${USER}/levi.git
        cd levi
        # Answer 'y' if it asks you to trust the .rvmrc file.
        gem env gemdir

    If you are using rvm, that should show something like:
        ~/.rvm/gems/ruby-1.9.2-p0@levi

1. Next:
        git remote add upstream git://github.com/roy98102/levi.git
        gem install bundler
        bundle install
        rails server -p 3000

1. Visit:
    [http://localhost:3000](http://localhost:3000)

You should see the default Rails welcome screen:
> Welcome aboard
>
> You're riding Ruby on Rails!
>
> ...

## General guidelines.

* For commit messages, always give a summary line, then a blank line, then whatever details you want. E.g.

        git commit
        ---<editor starts up>---
        Added killer featureX.

        - Ported to Python.
        - Switched language to Turkish.

* (This is a Work In Progress.)

## Integration procedure.

We are using the *Integration Manager* workflow [Figure 5-2](http://progit.org/book/ch5-1.html).

1. Develop a feature in a branch.

        git checkout -b feature master

1. When done, push the branch to your GitHub repo.

        git push origin feature

1. Within your levi fork on GitHub, issue a *pull request*.
1. Anyone can comment on the code. Converse! Look for errors, not style.
1. Any "Integration Manager" (anyone listed as a collaborator on the roy98102/levi repo) will test the commits, as described at GitHub at the bottom of the page where the *pull request* is discussed. It says this:

    > How to merge this pull request (called `feature` from `cdunn2001`):

   1. Check out a new branch to test the changes — run this from your project directory
 
            git clone git@github.com:roy98102/levi.git levi
	    cd levi
            git checkout -b cdunn2001-feature master

   2. Bring in cdunn2001's changes and test
     
            git pull https://cdunn2001@github.com/cdunn2001/pulltest.git feature
    
   3. Merge the changes and update the server
     
            git checkout master
            git merge cdunn2001-feature
            git push origin master

    4. With that, the `feature` branch will *not* exist in roy98102, which is good. Only the changes on it have been merged into the `master` branch. 

1. You (and others) may then pull in the latest master from roy98102.

	git remote add upstream git://github.com/roy98102/levi.git
	git fetch upstream
        git checkout master
        git merge upstream/master
	git push origin master

1. At that point, the submitter may delete the feature branch from his own repo.

        git checkout master
        git br -d feature
        git push origin :feature # to delete from GitHub

That's the full solution, but we can skip steps for simple changes that do not require testing. For those simple cases, we can take advantage of GitHub's [fork queues](https://github.com/blog/270-the-fork-queue). With that, the merge can occur entirely within GitHub.

The strange thing about the fork-queue is that *any* push you do to your GitHub repo will show up in the fork-queue. That makes your GitHub repo (usually called `origin`) very public.

### Simpler integration
Here are the simplified steps:

1. Develop on a feature branch.
1. Push to GitHub.
1. At GitHub, click on "Pull" to issue a *pull request*.
1. Someone logs into roy98102 and checks the fork-queue. (I use Chrome "Incognito Mode" for this.)
    * If the change is simple, he applies it to `master` and updates the branch, all in GitHub.
    * You will see the merge-commit on your own fork-queue, but you can ignore that.
1. Pull the change into you local `master`.
        git fetch origin
        git checkout master
        git merge origin/master
1. Delete your feature branch, if you want.

Try a few simple pull requests on your own `experimental` branch. I'll merge them into a throw-away `trash` branch for now. Use `gitx` to see what happens to your tree after you fetch the results.

Remember: Branch early and often!

### Notes
* [Useful cheatsheet.](http://cheat.errtheblog.com/s/git)
* I am working on these notes by modifying these notes.

