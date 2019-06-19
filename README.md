

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

