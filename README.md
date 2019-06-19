

<p align="center">
 <strong> Do-s-and-Dont-s-for-Git </strong>
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

- [Do read about git]
- [Do commit early and often]
- [Don’t panic]
- [Don’t change published history]
- [Do choose a workflow]
- [Miscellaneous “Do”s]
- [Miscellaneous “don’t”s]
- [Do enforce standards]
- [Do use useful tools]



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


## Don’t panic
As long as you have committed your work (or in many cases even added it with `git add`) your work will not be lost for at least two weeks unless you really work at it (run commands that manually purge it).

There are three places where “lost” changes can be hiding.

- **Reflog**.The reflog is where you should look first and by default. It shows you each commit that modified the git repository. 
```_`gitk --all --date-order $(git log -g --pretty=%H).`_
- **Lost and found**.Commits or other git data that are no longer reachable through any reference name (branch, tag, etc) are called “dangling” and may be found using `fsck`.
- **Dangling Commit**.These are the most likely candidates for finding lost data. A dangling commit is a commit no longer reachable by any branch or tag. 
```_`gitk --all --date-order $(git fsck | grep "dangling commit" | awk '{print $3;}')`_
- **Stashes**.Finally, you may have stashed the data instead of committing it and then forgotten about it. You can use the git stash list command or inspect them visually using. 
```_`gitk --all --date-order $(git stash list | awk -F: '{print $1};')`_
- **Misplaced**.Another option is that your commit is not lost. Perhaps the commit was just made on a different branch from what you remember.Using `git log -Sfoo --all` and `gitk --all --date-order` to try and hunt for your commits on known branches. 
- **Look elsewhere**.Finally, you should check your backups, testing copies, ask the other people who have a copy of the repo, and look in other repos.




