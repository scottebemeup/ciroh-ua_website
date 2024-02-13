The Case for Code Versioning
============================
* Versioning maintains snapshots of edited code, over time, with the ability to move forward and backward along that timeline
  * Save your brilliant idea for the whole team to use
  * Undo that unfortunate choice that ignored a fundamental assumption
* The timeline may include forks and mergers of experiments tried and abandoned or propagated
  * Try three things, test them in parallel, and keep the one you like best
  * Change your mind and pick the other option that was almost as fast, but is more flexible
* A single developer may benefit from code versioning, but a team of developers jointly modifying pieces of one project is likely to not succeed without code versioning
  * That elegant algorithm your teammate wrote can't be used until you share your updated data prep step
  * The person testing the code you shared last week needs a quick fix, but you are half way through a new, major update

![github_flow](/uploads/7870dbc5d076e1012f41d8165155fbd3/github_flow.png)

GIT for Code Versioning
=======================
* GIT is a Utility/App/Program to facilitate managing code versions
* First created in 2005 as part of Linux Development Environment
* Support Multiple Local Repositories that can be Conditionally Synchronized with each other
* Each Developer can have their own copy of everything, and can share updates with all, or some of, the other developers as they are ready for use

Basic Git Commands
------------------
* git **clone** : to create a local repository connected to a remote copy
  * Often points to a central copy referenced as the "Origin"
  * **git clone git@gitlab.uvm.edu:vermont-epscor/cyberinfrastructure.git cyberinf**
* git **status** : to assess the state of a local repository
  * List any untracked files or tracked files with uncommitted changes
* git **add** : to add a new or updated file to the list of updates to be tracked
   * Adds a file to the list to be included in the next commit
* git **commit** : to formally commit a set of updates to a new snapshot of content
  * Bundle all pending added changes into a retrievable snapshot
* git **push** : share an updated local repository to update the central copy
* git **pull** : update a local repository with updates from the central copy

![four_stages](/uploads/369a34cccf337633fbce31f4d2d21ca9/four_stages.png)

Some GIT Tutorials
------------------

* Software Carpentry 3 Hour Workshop
  * https://swcarpentry.github.io/git-novice/

GitLab : A Web Wrapper for GIT use
==================================
* GitLab is similar in look and feel to GitHub running on a local server
  * UVM has a GitLab Server, https://gitlab.uvm.edu/
  * Projects are Defined
  * GIT Repositories Created as part of Projects
  * Management of User Access and Authority
  * Support for Authoring Wiki Pages Associated with Projects

EPSCoR Projects 
---------------

![gitlabmain](/uploads/b286e52c31447182dca5fd76af6d1ed2/gitlabmain.jpg)

Your GitLab Profile
-------------------

* What Projects You Have Contributed To
* History of Activities in a List and a TimeLine

![gitlabprofile](/uploads/a0460c334cb1c0ad882237cc4fe84460/gitlabprofile.jpg)

Inside A GitLab Project
-----------------------

* Access to the Project repository
  * The URL to use to clone the project to a local repository
     * For example, git clone git@gitlab.uvm.edu:vermont-epscor/cyberinfrastructure.git cyberinf
  * Readme is displayed
  * Repository content selectable


![gitlabrepos](/uploads/cd4c1d4cd4352625c78bc964cc1c4a4b/gitlabrepos.jpg)

* Access to the Project Wiki (this page is part of a Project Wiki)
* Management of Project Members and Groups

![gitlabmembers](/uploads/31d5eadc5b58a5320f1ea887721ed33b/gitlabmembers.jpg)

