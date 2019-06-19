

<p align="center">
 <strong> Do's and Dont's for Git </strong>
    <br>
    <small>Git <code>.Do's and Dont's</code> template</small>
</p>
<br>
<p align="center">
    <a href="https://travis-ci.org/dvcs/gitignore"><img src="https://img.shields.io/travis/dvcs/gitignore.svg?longCache=true&style=flat-square" alt="build status"></a>
</p>


## About

Git is a flexible and powerful version control system. While Git offers significant functionality over legacy centralized tools like CVS and Subversion, it also presents so many options for workflow that it can be difficult to determine what is the best method to commit code to a project to follow and what are do’s and don’ts. 
The following are the guidelines I like to use for most software projects contained within a Git repository. 


## Table of Contents

- [Do read about git](#do-read-about-git)
- [Do commit early and often](#do-commit-early-and-often)
- [Don’t panic](#don’t-panic)
- [Don’t change published history](#don’t-change-published-history)
- [Do choose a workflow](#do-choose-a-workflow)
- [Miscellaneous “Do”s](#miscellaneous-“Do”s)
- [Miscellaneous “don’t”s](#miscellaneous-“Don’t”s)
- [Do enforce standards](#do-enforce-standards)
- [Do use useful tools](#do-use-useful-tools)
- [Reference Links](#reference-links)



## Do read about git
Knowing where to look is half the battle. I strongly urge everyone to read (and support) the Pro Git book. The other resources are highly recommended by various people as well.

- [Pro Git]( http://git-scm.com/book/)
- [Git for Computer Scientists](http://eagain.net/articles/git-for-computer-scientists/) and a [different/updated version](http://sitaramc.github.com/gcs/)
- [Git from the Bottom Up](https://jwiegley.github.io/git-from-the-bottom-up/)
- [The Git Parable](http://tom.preston-werner.com/2009/05/19/the-git-parable.html)
- [Other resources](http://git-scm.com/documentation)
- [Git wiki](http://git.wiki.kernel.org/)


## Do commit early and often
Git only takes full responsibility for your data when you commit. 
If you fail to commit and then do something poorly thought out, you can run into trouble. 
Additionally, having periodic checkpoints means that you can understand how you broke something.


_`Commit Early And Often`_. If, after you are done with no breaking changes. 
I prefer to commit in order to avoid future merge changes. Don’t let tomorrow’s beauty stop you from performing continuous commits today.
Some of the commands which comes handy while committing your work are 


```
# git add –all (add all files to stage ie changes files as well as newly added files)
# git status (to check if all files added or not. Easy check is every file will be in green color)
# git commit –a –m “well defined message to understand what you are committing to source code”.
```

## Don’t panic
As long as you have committed your work (or in many cases even added it with `git add`) your work will not be lost for at least two weeks unless you really work at it (run commands that manually purge it).

There are three places where “lost” changes can be hiding.

- **Reflog**.The reflog is where you should look first and by default. It shows you each commit that modified the git repository. 
```_`gitk --all --date-order $(git log -g --pretty=%H).`_```

- **Lost and found**.Commits or other git data that are no longer reachable through any reference name (branch, tag, etc) are called “dangling” and may be found using `fsck`.

- **Dangling Commit**.These are the most likely candidates for finding lost data. A dangling commit is a commit no longer reachable by any branch or tag. 
```_`gitk --all --date-order $(git fsck | grep "dangling commit" | awk '{print $3;}')`_```

- **Stashes**.Finally, you may have stashed the data instead of committing it and then forgotten about it. You can use the git stash list command or inspect them visually using. 
```_`gitk --all --date-order $(git stash list | awk -F: '{print $1};')`_```

- **Misplaced**.Another option is that your commit is not lost. Perhaps the commit was just made on a different branch from what you remember.Using `git log -Sfoo --all` and `gitk --all --date-order` to try and hunt for your commits on known branches. 

- **Look elsewhere**.Finally, you should check your backups, testing copies, ask the other people who have a copy of the repo, and look in other repos.




## Don’t change published history
Once you `git push` If you later find out that you messed up, make new commits that fix the problems




## Do choose a workflow
I am not going to specifically espouse one specific workflow as the best practice for using git since it depends heavily on the size and type of project and the skill of users, developers etc; 
However both reflexive avoidance of branches due to stupidity of other SCM systems and reflexive overuse of branches (since branches are actually easy with git) is most likely ignorance. 
Pick the style that best suits your project and don’t complain about user’s tactical uses of private branches.

1. **_Branch workflows_**
       Answering the following questions helps you choose a branch workflow
       - •	Where do important phases of development occur?
       - •	How can you identify (and backport) groups of related change?
       - •	Do you have work which often needs to be updated in multiple distinct long-lived branches?
       - •	What happens when emergency patches are required?
       - •	What should a branch for a particular purpose (including user-tactical) be named?
       - •	What is the lifecycle of a branch?

       See the following references for more information on branch workflows.
       - •	[Pro Git branching models](http://git-scm.com/book/ch3-4.html)
       - •	[Git-flow branching model](http://nvie.com/posts/a-successful-git-branching-model/) (with [the associated gitflow tool](https://github.com/petervanderdoes/gitflow-avh))
       - •	[Gitworkflows man page](http://jk.gs/gitworkflows.html)
       - •	[A Git Workflow for Agile Teams](http://reinh.com/blog/2009/03/02/a-git-workflow-for-agile-teams.html)
       - •	[What git branching models actually work](http://stackoverflow.com/questions/2621610/what-git-branching-models-actually-work)
       - •	[Our New Git Branching Model](http://blogs.remobjects.com/blogs/mh/2011/08/25/p2940)
       - •	[Branch-per-Feature](http://blogs.remobjects.com/blogs/mh/2011/08/25/p2940)
       - •	[Who Needs Process](http://widgetsandshit.com/teddziuba/2011/12/process.html)

2. **_Release tagging_**
      Choosing your release workflow (how to get the code to the customer) is another important decision. You should have already considered most of the issues when going over the branching and distributed workflow above, but less obviously, it may affect how and when you perform tagging, and specifically the name of the tag you use.
      ```https://git-scm.com/book/en/v2/Git-Basics-Tagging```

      Repositories sometimes get used to store things that they should not, simply because they were there. Try to avoid doing so.

     **•	One conceptual group per repository.** Does this mean one per product, program, library, class? Only you can say. However, dividing stuff up later is annoying and leads to rewriting public history or duplicative or missing history. Dividing it up correctly beforehand is much better.

     **•	Read access control is at the repo level**If someone has access to a repository, they have access to the entire repo, all branches, all history, everything. If you need to compartmentalize read access, separate the compartments into different repositories.
     
     **• Separate repositories for files that might be needed by multiple projects**  This promotes sharing and code reuse, and is highly recommended.

     **•	Separate repositories for planned continual history rewrites** You will note that I have already recommended against rewriting public history. Well, there are times when doing that just makes sense. One example might be a cache of pre-built binaries so that most people don’t need to rebuild them. Yet older versions of this cache (or at least older versions not at tag boundaries) may be entirely useless and so you want to pretend they never happened to save space. You can rebase, filter, or squash these unwanted commits away, but this is rewriting history and can cause problem. So if you really must do so, isolate these files into a repository so that at least everything else will not be affected.

     **•	Group concepts into a superproject** Once you have divided, now you need to conquer. You can assemble multiple individual repositories into a superproject to group all of the concepts together to create your unified work.

_There are two main methods of doing this:_
      _a.	git-submodules_ 
        Git submodules is the native git approach, which provides a strong binding between the superproject repository and the     subproject repositories for every commit. This leads to a baroque and annoying process for updating the subproject. However, if you do not control the subproject (solvable by “forking”) or like to perform blame-based history archeology where you want to find out the absolute correspondence between the different projects at every commit, it is very useful.
      _b.	git slave_ 
        Gitslave is a useful tool to add a subsidiary git repositories to a git superproject when you control and develop on the subprojects at more or less the same time as the superproject, and furthermore when you typically want to tag, branch, push, pull, etc all repositories at the same time. There is no strict correspondence between superproject and subproject repositories except at tag boundaries (though if you need to look back into history you can usually guess pretty well and in any case this is rarely needed).



## Miscellaneous “Do”s
These are random best practices that are too minor or disconnected to go in any other section.
**•	Always have `.gitignore` root of your project.**
     o	This file will make sure for not pushing or committing any junk or local data to your repo.
     o	You can follow some of the predefined template for gitignore file
     o	[https://www.atlassian.com/git/tutorials/saving-changes/gitignore](https://www.atlassian.com/git/tutorials/saving-changes/gitignore)
     o	[https://git-scm.com/docs/gitignore](https://git-scm.com/docs/gitignore)
     o	[https://github.com/github/gitignore](https://github.com/github/gitignore) (this is most useful as it contain lot of template) 

**•	Copy/move a file in a different commit from any changes to it**
    If you care about git properly displaying the fact that you moved a file, you should copy or move the file in a different commit from any changes you need to immediately make to that file. 
    This is because git does not record ```git mv``` any different from a delete and an add, and because ```git cp``` doesn’t even exist. 
    Git’s output commands are the ones that interpret the data as a move or copy. See the -C and -M options to ```git log```(and similar commands).
    
**•	(Almost) Always name your stashes**
    If you don’t provide a name when stashing, git generates one automatically based on the previous commit. 
    While this tells you the branch where a stash was made, it gives you no idea what is in it. 
    Unless you plan to pop a stash in the next few minutes, you should always give it a name with ```git stash save XXX``` rather than the shorter default ```git stash``` (which should be reserved for very temporary uses). 
    This way you’ll have some idea what a stash is about when you are looking at it months later.
**•	Protect your bare/server repos against history rewriting**
    If you initialize a bare git repository with “–shared” it will automatically get the ```git-config``` “receive.denyNonFastForwards” set to true. 
    You should ensure that this is set just in case you did something weird during initialization. Furthermore, you should also set “receive.denyDeletes” so that people who are trying to rewrite history cannot simply delete the branch and then recreate it. 
    **Best practice** is for there to be a speedbump any time someone is trying to delete or rewrite history, since it is such a bad idea.
**•	Experiment!**
    When you have an idea or are not sure what something does, try it out! 
    Ideally try it out in a clone or copy so that recovery is trivial. 
    While you can normally completely recover from any git experiment involving data that has been fully committed, perhaps you have not committed yet or perhaps you are not sure whether something falls in the category of “trying hard” to destroy history.


## Miscellaneous “Don’t”s
In this list of things to _not_ do, it is important to remember that there are legitimate reasons to do all of these. However, you should not attempt any of these things without understanding the potential negative effects of each and why they might be in a best practices **“Don’t”** list.

**_DO NOT_**
**_•	Commit anything that can be regenerated from other things that were committed**_
     Things that can be regenerated include binaries, object files, jars, .class, flex/yacc generated code, etc. 
     Really the only place there is room for disagreement about this is if something might take hours to regenerate (rendered images, e.g., but see [Dividing work into repositories](https://sethrobertson.github.io/GitBestPractices/#divide) for more best practices about this) or autoconf generated files (so people can configure and compile without autotools installed).
     
**_•	commit configuration files_**
     Specifically configuration files that might change from environment to environment or for any reasons. See [Information about local versions of configuration files](https://gist.github.com/1423106)
     
**_•	use git as a web deployment tool_**
     Yes it can be done in a sufficiently simple/non-critical environment with something like [Abhijit Menon-Sen’s document on using git to manage a web site](http://toroid.org/ams/git-website-howto) to help, though there are [other examples](http://joemaller.com/990/a-web-focused-git-workflow/). 
     However, this does not give you atomic updates, synchronized db updates, or other accouterments of an industrial deployment system.
     
**_•	commit large binary files (when possible)_**
    Large is currently relative to the amount of free RAM you have. Remember that not everyone may be using the same memory configuration you are. Support for large files is an active git topic, so watch for changes.
    After running a git gc you should be able to find the largest objects by running:
    ```
    git verify-pack -v .git/objects/pack/pack-*.idx |
    grep blob | sort -k3nr | head |
    while read s x b x; do
      git rev-list --all --objects | grep $s |
      awk '{print "'"$b"'",$0;}';
    done
    ```
    Consider using [Git annex](http://git-annex.branchable.com/) or [Git media](https://github.com/schacon/git-media) if you plan on having large binary files and your workflow allows.

**_•	create very large repositories (when possible)_**
   Git can be slow in the face of large repositories. The definition of “large” will depend on your RAM size, I/O speed, expectations, etc. However, having 100K-200K files in a repository may slow common operations due to stat system call speeds (especially on Windows) and having many large (esp. binary) files (see above) can slow many operations.

   If you start having pack files (in ```.git/objects/pack```) which are larger than 1GB, you might also want to consider creating a .keep file (right beside the ```.idx``` and ```.pack``` files) for a large pack which will prevent them from being repacked during gc and repack operations.
   
   If you find yourself running into memory pressure when you are packing commits (usually ```git gc [--aggressive]```), there are git-config options that can help. ```pack.threads=1 pack.deltaCacheSize=1pack.windowMemory=512m``` all of which trade memory for CPU time. Other likely ones exist. My gut tells me that sizing (“deltaCacheSize” + “windowMemory” + min(“core.bigFileThreshold[512m]”, TheSizeOfTheLargestObject)) * “threads” to be around half the amount of RAM you can dedicate to running git gc will optimize your packing experience, but I will be the first to admit that made up that formula based on a very few samples and it could be drastically wrong.
   Support for large repositories is an active git topic, so watch for changes.

**_•	use ```reset (--hard | --merge) ```without committing/stashing_**
    This can often overwrite the working directory without hope of recourse.

**_•	use ```checkout``` in file mode_**
    This will overwrite some (or potentially all with .) of the working directory without hope of recourse.

**_•	use ```git clean``` without previously running with “-n” first_**
    This will delete untracked files without hope of recourse.

**_•	prune the reflog_**
    This is removing your safety belt.

**_•	expire “now”_**
    This is cutting your safety belt.

**_•	use ```git repack -ad```_**
    Unreferenced objects in a newly redundant pack will get deleted which cuts your safety belt. Instead use git gc or at least git repack -Ad

**_•	use a branch argument to ```git pull or git fetch```_**
    No doubt there is a good use case for, say, git pull origin master or whatever, but I have yet to understand it. What I do understand is that every time I have seen someone use it, it has ended in tears.

**_•	use git as a generic filesystem backup tool_**
    Git was not written as a dedicated backup tool, and such tools do exist. Yes people have done it successfully, but usually with lots of scripts or modifications around it. One successful example of integration/modifications is [bup](http://github.com/apenwarr/bup).

**_•	rewrite public history_**
    See [section about this topic](https://sethrobertson.github.io/GitBestPractices/#pubonce). It bears repeating, though.

**_•	change where a tag points_**
    This is another way to rewrite public history.

**_•	use ```git-filter-branch```_**
    Still another way to [rewrite public history](https://sethrobertson.github.io/GitBestPractices/#pubonce).
    However, if you are going to use git-filter-branch, make sure you end your command with ` –tag-name-filter cat – –all` unless you are really really sure you know what you are doing.

**_•	create ```--orphan``` branches**_
    With the notable exception of gh-pages (which is a hack github uses for convenience, not an expression of general good style practice), any situation where creating an orphan branch seems like a reasonable solution you probably should just create a new repository. If the new branch cannot really be thought of as being related to the other branches in your repository so that merging between the two really has any conceptual relevance, then the concept is probably far enough apart to warrant its own repository.

**_•	use ```clone --shared or --reference```**_
    This can lead to problems for non-normal git actions, or if the other repository is deleted/moved. See [git-clone manual page](http://jk.gs/gitworkflows.html).

**_•	use git-grafts**_
    This is deprecated in favor of ```git-replace```.

**_•	use git-replace**_
    But don’t use ```git-replace``` either.
    
    
## Do enforce standards
See [Puppet Version Control](http://projects.puppetlabs.com/projects/1/wiki/Puppet_Version_Control) for an example for a _“Git Update Hook” and “Git Pre-Commit Hook”_ that enforces certain standards. 


## Do use useful tools
More than useful, use of these tools may help you form a best practice!

  **•	[gitolite](https://github.com/sitaramc/gitolite)**
  We already mentioned gitolite above, but it forms a great git server intermediary for access control.
  **•	[gitslave](http://gitslave.sf.net/)**
  We already mentioned gitslave above, but it forms a great alternative to git-submodules when forming superprojects out of repositories you control.
  **•	[gerrit](http://code.google.com/p/gerrit/)**
  To quote the website: Gerrit is a web based code review system, facilitating online code reviews for projects using the Git version control system.


## Reference Links
- [https://davidwalsh.name/45-github-issues-dos-donts](https://davidwalsh.name/45-github-issues-dos-donts)
- [Git Best Practices: Workflow Guidelines](https://www.lullabot.com/articles/git-best-practices-workflow-guidelines)
- [Follow these simple rules and you’ll become a Git and GitHub master](https://www.freecodecamp.org/news/follow-these-simple-rules-and-youll-become-a-git-and-github-master-e1045057468f/)
- [Don’t Mess with the Master](https://thenewstack.io/dont-mess-with-the-master-working-with-branches-in-git-and-github/)



