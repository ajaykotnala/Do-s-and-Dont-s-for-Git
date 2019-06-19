Git Do’s and Don’ts
Git is a flexible and powerful version control system. While Git offers significant functionality over legacy centralized tools like CVS and Subversion, it also presents so many options for workflow that it can be difficult to determine what is the best method to commit code to a project to follow and what are do’s and don’ts. 
The following are the guidelines I like to use for most software projects contained within a Git repository. 

Do read about git
Knowing where to look is half the battle. I strongly urge everyone to read (and support) the Pro Git book. The other resources are highly recommended by various people as well.
•	Pro Git
•	Git for Computer Scientists and a different/updated version
•	Git from the Bottom Up
•	The Git Parable
•	Other resources
•	Git wiki

Do commit early and often
Git only takes full responsibility for your data when you commit. If you fail to commit and then do something poorly thought out, you can run into trouble. Additionally, having periodic checkpoints means that you can understand how you broke something.
Commit Early And Often. If, after you are done with no breaking changes. I prefer to commit in order to avoid future merge changes. Don’t let tomorrow’s beauty stop you from performing continuous commits today.
Some of the commands which comes handy while committing your work are 
git add –all (add all files to stage ie changes files as well as newly added files)
git status (to check if all files added or not. Easy check is every file will be in green color)
git commit –a –m “well defined message to understand what you are committing to source code”.

Don’t panic
As long as you have committed your work (or in many cases even added it with git add) your work will not be lost for at least two weeks unless you really work at it (run commands that manually purge it).

There are three places where “lost” changes can be hiding.
•	Reflog
The reflog is where you should look first and by default. It shows you each commit that modified the git repository. 
      gitk --all --date-order $(git log -g --pretty=%H).

•	Lost and found
Commits or other git data that are no longer reachable through any reference name (branch, tag, etc) are called “dangling” and may be found using fsck.

•	Dangling Commit
	These are the most likely candidates for finding lost data. A dangling commit is a commit no longer reachable by any branch or tag.
	gitk --all --date-order $(git fsck | grep "dangling commit" | awk '{print $3;}')




•	Stashes
o	Finally, you may have stashed the data instead of committing it and then forgotten about it. You can use the git stash list command or inspect them visually using:
o	gitk --all --date-order $(git stash list | awk -F: '{print $1};')

•	Misplaced
Another option is that your commit is not lost. Perhaps the commit was just made on a different branch from what you remember. Using git log -Sfoo --all and gitk --all --date-order to try and hunt for your commits on known branches.
•	Look elsewhere
Finally, you should check your backups, testing copies, ask the other people who have a copy of the repo, and look in other repos.


Don’t change published history
Once you git push If you later find out that you messed up, make new commits that fix the problems


Do choose a workflow
I am not going to specifically espouse one specific workflow as the best practice for using git since it depends heavily on the size and type of project and the skill of users, developers etc; 
however both reflexive avoidance of branches due to stupidity of other SCM systems and reflexive overuse of branches (since branches are actually easy with git) is most likely ignorance. 
Pick the style that best suits your project and don’t complain about user’s tactical uses of private branches.


Branch workflows
Answering the following questions helps you choose a branch workflow:
•	Where do important phases of development occur?
•	How can you identify (and backport) groups of related change?
•	Do you have work which often needs to be updated in multiple distinct long-lived branches?
•	What happens when emergency patches are required?
•	What should a branch for a particular purpose (including user-tactical) be named?
•	What is the lifecycle of a branch?
See the following references for more information on branch workflows.
•	Pro Git branching models
•	Git-flow branching model (with the associated gitflow tool)
•	Gitworkflows man page
•	A Git Workflow for Agile Teams
•	What git branching models actually work
•	Our New Git Branching Model
•	Branch-per-Feature
•	Who Needs Process

Release tagging
Choosing your release workflow (how to get the code to the customer) is another important decision. You should have already considered most of the issues when going over the branching and distributed workflow above, but less obviously, it may affect how and when you perform tagging, and specifically the name of the tag you use.
https://git-scm.com/book/en/v2/Git-Basics-Tagging

Repositories sometimes get used to store things that they should not, simply because they were there. Try to avoid doing so.
•	One conceptual group per repository.
Does this mean one per product, program, library, class? Only you can say. However, dividing stuff up later is annoying and leads to rewriting public history or duplicative or missing history. Dividing it up correctly beforehand is much better.
•	Read access control is at the repo level
If someone has access to a repository, they have access to the entire repo, all branches, all history, everything. If you need to compartmentalize read access, separate the compartments into different repositories.
•	Separate repositories for files that might be needed by multiple projects
This promotes sharing and code reuse, and is highly recommended.
•	Separate repositories for large binary files
Git doesn’t handle large binary files ideally yet and large repositories can be slow. If you must commit them, separating them out into their own repository can make things more efficient.
•	Separate repositories for planned continual history rewrites
You will note that I have already recommended against rewriting public history. Well, there are times when doing that just makes sense. One example might be a cache of pre-built binaries so that most people don’t need to rebuild them. Yet older versions of this cache (or at least older versions not at tag boundaries) may be entirely useless and so you want to pretend they never happened to save space. You can rebase, filter, or squash these unwanted commits away, but this is rewriting history and can cause problem. So if you really must do so, isolate these files into a repository so that at least everything else will not be affected.
•	Group concepts into a superproject
Once you have divided, now you need to conquer. You can assemble multiple individual repositories into a superproject to group all of the concepts together to create your unified work.
There are two main methods of doing this.
o	git-submodules
Git submodules is the native git approach, which provides a strong binding between the superproject repository and the subproject repositories for every commit. This leads to a baroque and annoying process for updating the subproject. However, if you do not control the subproject (solvable by “forking”) or like to perform blame-based history archeology where you want to find out the absolute correspondence between the different projects at every commit, it is very useful.
o	gitslave
gitslave is a useful tool to add a subsidiary git repositories to a git superproject when you control and develop on the subprojects at more or less the same time as the superproject, and furthermore when you typically want to tag, branch, push, pull, etc all repositories at the same time. There is no strict correspondence between superproject and subproject repositories except at tag boundaries (though if you need to look back into history you can usually guess pretty well and in any case this is rarely needed).
Miscellaneous “Do”s
These are random best practices that are too minor or disconnected to go in any other section.
•	(Almost) Always have .gitignore root of your project.
o	This file will make sure for not pushing or committing any junk or local data to your repo.
o	You can follow some of the predefined template for gitignore file
o	https://www.atlassian.com/git/tutorials/saving-changes/gitignore
o	https://git-scm.com/docs/gitignore
o	https://github.com/github/gitignore (this is most useful as it contain lot of template)

•	Copy/move a file in a different commit from any changes to it
If you care about git properly displaying the fact that you moved a file, you should copy or move the file in a different commit from any changes you need to immediately make to that file. This is because git does not record git mv any different from a delete and an add, and because git cp doesn’t even exist. Git’s output commands are the ones that interpret the data as a move or copy. See the -C and -M options to git log(and similar commands).
•	(Almost) Always name your stashes
If you don’t provide a name when stashing, git generates one automatically based on the previous commit. While this tells you the branch where a stash was made, it gives you no idea what is in it. Unless you plan to pop a stash in the next few minutes, you should always give it a name with git stash save XXX rather than the shorter default git stash (which should be reserved for very temporary uses). This way you’ll have some idea what a stash is about when you are looking at it months later.
•	Protect your bare/server repos against history rewriting
If you initialize a bare git repository with “–shared” it will automatically get the git-config “receive.denyNonFastForwards” set to true. You should ensure that this is set just in case you did something weird during initialization. Furthermore, you should also set “receive.denyDeletes” so that people who are trying to rewrite history cannot simply delete the branch and then recreate it. Best practice is for there to be a speedbump any time someone is trying to delete or rewrite history, since it is such a bad idea.
•	Experiment!
When you have an idea or are not sure what something does, try it out! Ideally try it out in a clone or copy so that recovery is trivial. While you can normally completely recover from any git experiment involving data that has been fully committed, perhaps you have not committed yet or perhaps you are not sure whether something falls in the category of “trying hard” to destroy history.
Miscellaneous “don’t”s
In this list of things to not do, it is important to remember that there are legitimate reasons to do all of these. However, you should not attempt any of these things without understanding the potential negative effects of each and why they might be in a best practices “Don’t” list.
DO NOT
•	commit anything that can be regenerated from other things that were committed.
Things that can be regenerated include binaries, object files, jars, .class, flex/yacc generated code, etc. Really the only place there is room for disagreement about this is if something might take hours to regenerate (rendered images, e.g., but see Dividing work into repositories for more best practices about this) or autoconf generated files (so people can configure and compile without autotools installed).
•	commit configuration files
Specifically configuration files that might change from environment to environment or for any reasons. See Information about local versions of configuration files
•	use git as a web deployment tool
Yes it can be done in a sufficiently simple/non-critical environment with something like Abhijit Menon-Sen’s document on using git to manage a web site to help, though there are other examples. However, this does not give you atomic updates, synchronized db updates, or other accouterments of an industrial deployment system.
•	commit large binary files (when possible)
Large is currently relative to the amount of free RAM you have. Remember that not everyone may be using the same memory configuration you are. Support for large files is an active git topic, so watch for changes.
After running a git gc you should be able to find the largest objects by running:
git verify-pack -v .git/objects/pack/pack-*.idx |
grep blob | sort -k3nr | head |
while read s x b x; do
  git rev-list --all --objects | grep $s |
  awk '{print "'"$b"'",$0;}';
done
Consider using Git annex or Git media if you plan on having large binary files and your workflow allows.
•	create very large repositories (when possible)
Git can be slow in the face of large repositories. The definition of “large” will depend on your RAM size, I/O speed, expectations, etc. However, having 100K-200K files in a repository may slow common operations due to stat system call speeds (especially on Windows) and having many large (esp. binary) files (see above) can slow many operations.
If you start having pack files (in .git/objects/pack) which are larger than 1GB, you might also want to consider creating a .keep file (right beside the .idx and .pack files) for a large pack which will prevent them from being repacked during gc and repack operations.
If you find yourself running into memory pressure when you are packing commits (usually git gc [--aggressive]), there are git-config options that can help. pack.threads=1 pack.deltaCacheSize=1pack.windowMemory=512m all of which trade memory for CPU time. Other likely ones exist. My gut tells me that sizing (“deltaCacheSize” + “windowMemory” + min(“core.bigFileThreshold[512m]”, TheSizeOfTheLargestObject)) * “threads” to be around half the amount of RAM you can dedicate to running git gc will optimize your packing experience, but I will be the first to admit that made up that formula based on a very few samples and it could be drastically wrong.
Support for large repositories is an active git topic, so watch for changes.
•	use reset (--hard | --merge) without committing/stashing
This can often overwrite the working directory without hope of recourse.
•	use checkout in file mode
This will overwrite some (or potentially all with .) of the working directory without hope of recourse.
•	use git clean without previously running with “-n” first
This will delete untracked files without hope of recourse.
•	prune the reflog
This is removing your safety belt.
•	expire “now”
This is cutting your safety belt.
•	use git repack -ad
Unreferenced objects in a newly redundant pack will get deleted which cuts your safety belt. Instead use git gc or at least git repack -Ad
•	use a branch argument to git pull or git fetch
No doubt there is a good use case for, say, git pull origin master or whatever, but I have yet to understand it. What I do understand is that every time I have seen someone use it, it has ended in tears.
•	use git as a generic filesystem backup tool
Git was not written as a dedicated backup tool, and such tools do exist. Yes people have done it successfully, but usually with lots of scripts or modifications around it. One successful example of integration/modifications is bup.
•	rewrite public history
See section about this topic. It bears repeating, though.
•	change where a tag points
This is another way to rewrite public history.
•	use git-filter-branch
Still another way to rewrite public history.
However, if you are going to use git-filter-branch, make sure you end your command with ` –tag-name-filter cat – –all` unless you are really really sure you know what you are doing.
•	create --orphan branches
With the notable exception of gh-pages (which is a hack github uses for convenience, not an expression of general good style practice), any situation where creating an orphan branch seems like a reasonable solution you probably should just create a new repository. If the new branch cannot really be thought of as being related to the other branches in your repository so that merging between the two really has any conceptual relevance, then the concept is probably far enough apart to warrant its own repository.
•	use clone --shared or --reference
This can lead to problems for non-normal git actions, or if the other repository is deleted/moved. See git-clone manual page.
•	use git-grafts
This is deprecated in favor of git-replace.
•	use git-replace
But don’t use git-replace either.

Do enforce standards
See Puppet Version Control for an example for a “Git Update Hook” and “Git Pre-Commit Hook” that enforces certain standards. 

Do use useful tools
More than useful, use of these tools may help you form a best practice!
•	gitolite
We already mentioned gitolite above, but it forms a great git server intermediary for access control.
•	gitslave
We already mentioned gitslave above, but it forms a great alternative to git-submodules when forming superprojects out of repositories you control.
•	gerrit
To quote the website: Gerrit is a web based code review system, facilitating online code reviews for projects using the Git version control system.







