# Contributing to a GitHub open source project (from a Visual Studio developer perspective)

## Introduction

<img alt="GitHub logo" src="http://www.ghislainproulx.net/content/images/2014/GitHub-Mark-120px-plus.png" style="float:right;margin: 0 0 1em 1em;border:0;">

I was at the Microsoft //Build/ 2013 conference when [Mads Kristensen](http://madskristensen.net/) [turned his Web Essentials personal project into a public one](https://channel9.msdn.com/Events/Build/2013/3-503#time=52m15s). At this time, I had downloaded the code to take a look at it. But I did not find any simple ideas to start collaborating to this very useful tool. This year, at //Build/ 2014, he made a demonstration of new features of Web Essentials with Angular.js when I thought about adding validators for the Bootstrap framework.

The code is well maintained by a group of people very motivated to improve this tool.
Adding my small contributions was quite easy in comparison to using Git. I'm developing mostly exclusively with Microsoft's products since the beginning of my career, 15 years ago, so leaving my old habits of VSS and TFS to Git was not *natural* for me, to say the least. 

After a few contributions, and some challenges with Git, I decided to take a 
step back and take the time to have a better understanding of how to use it
correctly.

## So, learning Git

Let's start with a high level view of what it is and how it works for me. I'll explain all those steps in detail, one by one, later in this post.

![](http://www.ghislainproulx.net/content/images/2014/GitHub101.jpg)

### How Git works

The biggest advantage of Git, and maybe the more complex to figure out for a developer that usually uses TFS (like me), is the fact that Git is a distributed version control system. You have a local AND a remote repository.

Basically, when you commit some modifications, only your local repository will be updated. You have to push those modifications after if you want to update the server.

## GitHub != Git
[GitHub](http://www.github.com) is a very nice, simple but powerful web interface that sits on top of Git and adds [a lot of collaborative features](https://github.com/features). Most important features from an open source standpoint are:

* Integrated issue tracking
* Collaborative code review
* Text editor focused on collaboration

The first step to collaborate on a project hosted by GitHub is to [create an account](https://github.com/join). GitHub is free for all public repository. You have to pay only if you want a private one. 

In order to do the following steps you must have created your GitHub account and you have authenticated yourself on the web site.

### Fork a project

First step to contribute to an open source project on GitHub, you have to fork the project you want to contribute on. For that, find the project on GitHub and click the *Fork* button on the upper right corner. This will create a copy of the project repository on your own GitHub account.

![](http://www.ghislainproulx.net/content/images/2014/forkproject.png)

### Installing tools

[Phil Haack](http://www.github.com/haacked) and his colleagues from GitHub made a very interesting job with the [GitHub for Windows application](https://windows.github.com/). I installed it when I started exploring with GitHub and open source projects. After some time, I switched to the Git console because I felt I would have more control and I would understand better what was happening in my repository. The console application is installed at the same time that the GitHub for Windows application so I recommend you to install it as well. All other steps on this post will be explained with the Git shell. Your will find the link in the <code>GitHub</code> folder of the *Start Menu*.
 
### Clone to your local repository

Next step, download source code from your server repository to the local one on your computer. The operation is called *clone* on Git. On the Git shell, enter the command bellow. You will find the URL on the right-side menu of your GitHub repository page.

<code>git clone project_url</code>

![](http://www.ghislainproulx.net/content/images/2014/RepoURL.png)

### Branching

Branching is a big thing with Git and even more with GitHub because it allows you to send a pull-request by _feature_ and to work on many modifications in parallel without the need to submit all of them at the same time.

You can navigate between your <code>master</code> branch and your other branches by using the <code>checkout</code> command. You can also use this command to create a new branch by adding the <code>-b</code> parameter:

    git checkout -b newBranchName

This will create the new branch and set it as the active one at the same time. Git doesn't create a physical folder per branch on your drive as TFS does. It will only refresh the project folder based on the required files for this branch.

### Do your modifications

Back to normal! :-)  Open Visual Studio and do your best to improve the project.

### Check status of your branch

After you are done with your modifications, and before doing your commit, it's a good idea to check the state of your branch.

    git status

The result should look like that:

    C:\Users\GProulx\Documents\GitHub\WebEssentials2013 [MyNewAwesomeFeature +0 ~1 -0]> git status
    # On branch MyNewAwesomeFeature
    # Changes not staged for commit:
    #   (use "git add <file>..." to update what will be committed)
    #   (use "git checkout -- <file>..." to discard changes in working directory)
    #
    #       modified:   EditorExtensions/HTML/Validation/BootstrapColumnsValidator.cs
    #
    no changes added to commit (use "git add" and/or "git commit -a")
    C:\Users\GProulx\Documents\GitHub\WebEssentials2013 [MyNewAwesomeFeature +0 ~1 -0]>


### Commit

Once you are happy with your work it's time to commit it to your local repository. In Git you have to add files to your staging area before you can commit them, even if it is not a new file. The staging area is a simple file, generally contained in your Git directory, that stores information about what will go into your next commit.

For that, there are two options. The first one is to add each file individually with the <code>add</code> command. As you will need to enter the full name of the file, including the path, you can always use the [Tab] key in order to benefit of the auto-completion.

   
    git add Full_Name_Of_The_File

Or, you can tell Git to add them during the commit process by adding the <code>-a</code> argument before the <code>-m</code>.

    git commit -a -m "New feature for xyz"

### Push

As my initial diagram showed, the last step before being able to send your contribution is to push your commit(s) from your local machine to your GitHub repository. The push command requires the origin branch and the destination branch. If the destination branch doesn't exist yet, it will be created during the push process. 

For example, I already created a branch named MyNewAwesomeFeature only on my local repository. So, the push command to send my modifications on the server would look like this :

    git push origin MyNewAwesomeFeature

And the result of this command would be something similar to:

    Counting objects: 11, done.
    Delta compression using up to 8 threads.
    Compressing objects: 100% (6/6), done.
    Writing objects: 100% (6/6), 493 bytes | 0 bytes/s, done.
    Total 6 (delta 5), reused 0 (delta 0)
    To https://github.com/GProulx/WebEssentials2013.git
     * [new branch]      MyNewAwesomeFeature -> MyNewAwesomeFeature
    C:\Users\GProulx\Documents\GitHub\WebEssentials2013 [MyNewAwesomeFeature]> 

### Pull request

Sending a pull-request is the way to ask the owner of the GitHub project to check your contribution and, eventually, merge it in the original repository. 

This operation is done directly on your GitHub page. After the push, you will see a new section on your page with an indicator that it's time for a pull request!

![](http://www.ghislainproulx.net/content/images/2014/CompareAndPullRequest.png)

As Phil Haack explained it very well during his last appearance on the [.Net Rocks Podcast to talk about Open Source](http://www.dotnetrocks.com/default.aspx?showNum=1028), a pull-request is not necessarily the last step of your contribution. It is also a very useful way to initiate the conversation about what can be your contribution on a specific aspect of a project. 

Before creating your pull request, you should check the "Guidelines for contributing" for the current project if they have it. As shown on the next image, you will see a link to the guidelines if the project's owner has defined any. 

If everything seems OK, you should add a description of your contribution and create the pull request.

![](http://www.ghislainproulx.net/content/images/2014/CreatePullRequest.png)

### It's not over until it's merged!
It's important to remember that the pull request is linked to the branch and not to the source code as it was at the time of the pull-request. Every commit that you will do on that branch after the pull-request will be included in it as well, as long as your pull-request is not merged.

### And after the merge?
As already explained, working with feature branches is the easiest way to go. Now that your contribution has been merged by the owner of the project, you can delete your branch. To do that, you can use this command, that will delete your local branch.

    git branch -d MyNewAwesomeFeature

But, if you want a better way, you should check Phil Haack's blog post: [GitHub Flow Like a Pro with these 13 Git Aliases](http://haacked.com/archive/2014/07/28/github-flow-aliases/) where you can find many useful shortcuts. One of them, probably the most powerful, is <code>git bdone</code> who will:

1. Switches to master
2. Brings master up to speed with the origin
3. Deletes all branches already merged into master

So, after running this command, your are now ready to start another awesome contribution!

## Lost?

The Git documentation is very helpful and well explained (sometimes a little too much). To check the documentation about a specific command, just enter:

    git help <verb>

If you prefer the full documentation, it is available on the Git Web site at: [http://www.git-scm.com/doc](http://www.git-scm.com/doc)

## References 
* [Git documentation](http://www.git-scm.com/doc)
* [Git Book](http://git-scm.com/book) - Especially the [Getting Started - Git Basics](http://git-scm.com/book/en/Getting-Started-Git-Basics) section.
* Phil Haack [participated in many podcasts to talk about GitHub lately](http://haacked.com/archive/2014/09/08/podcasts/) and you can learn a lot about Git and what is coming.