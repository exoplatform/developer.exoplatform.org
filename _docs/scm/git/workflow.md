---
title: "Git - Workflow"
permalink: /docs/scm/git/workflow/
redirect_from:
  - /docs/scm/git-workflow.html
tags: [git,gitflow]
---

Our workflow is built on two principles :

* The **repository architecture** (development vs blessed) that has to be followed by **all projects involved in products** produced eXo (and thus that require to be supported).
* The **branching model** that has to be followed by *all projects* at eXo

## Repository architecture

Aiming security and backup purpose, we are using two repository kinds (owned by two distinct github organizations).

These are ```blessed``` and ```development``` repositories hosted respectively on [exoplatform](https://github.com/exoplatform) and [exodev](https://github.com/exodev) organizations.

Development repositories are forked from blessed repositories.

**This strategy is applied to all repositories/projects involved in eXo products.** Others projects are using a single repository hosted on "exoplatform" organization.

![image alt text](/assets/images/docs/scm/git-organization.png)

### Development repository

This repository is the developers repository. The main development branch is ```develop``` branch. Depending the contribution kind (one shot contribution or feature contribution), the developer can use a dedicated ```feature``` branch if needed.
The most of development activity will be done in this repository by a lot of contributors :

* ```maintainers``` (formerly known as ```sl3```) : To develop fix. These developments are done in dedicated ```fix``` branches (more details below).
* ```all development teams``` : To do one shot contribution and handle feature branch life cycle.

In this repository, ```develop``` branch and ```feature``` branch will be under CI. 

### Blessed repository

In this repository you can find ```stable``` branches and release tags. There is ```master``` branch also.
Only some people are able to write on this repository :

* ```maintainers``` : To integrate pull request on stable branches.
* ```release manager``` : To perform release operations on stable (supported) branches.
* ```keepers``` : Repository keepers are ```Project Leader```, ```Team Leader``` and ```Technical Leader```. They are able to pull changes from dev to blessed when the develop is stable enough and they can process releases on master branch for non supported versions of products (alpha, beta, RCs, ...)

The continuous integration is applied on stables branches (```stable/1.0.x```, ```stable/1.1.x```, etc) and ```master``` on blessed repository.

## Branching model

Branching model are 7 kinds of branch :

* ```master``` : Master branch always reflect a production ready state (for community website for instance). It’s a snapshot of the Develop Branch at a given time.
* ```develop``` : Develop branch contains the latest delivered development changes.
* ```feature/xxx``` : Feature branches are dedicated branch for one big feature (lot of commits), "xxx" is the feature name.
* ```stable/xxx``` : Stable branch are used to perform releases and write / accept fix. "xxx" is the stable version name (e.g 1.0.x).
* ```fix/xxx``` : Fix branch is dedicated to integrate bugfix on Develop branch. If needed the fix is then cherry pick on stable branch.
* ```integration/xxx``` : Integration branches are dedicated branch to automatic integration task (like Crowdin translation).
* ```poc/xxx``` : Poc branches are dedicated branch to develop a Prove of Concept (PoC).

### Master Branch

```Engineering```

Master branch always reflect a production ready state (for community website for instance). It’s a snapshot of the Develop Branch at a given time.

Commit directly to Master branch is FORBIDDEN (except exceptional circumstance: hotfix).

![image alt text](/assets/images/docs/scm/master-branch.png =400x)

## Develop Branch

```Engineering - GSS Vietnam```

Develop branch contains the latest delivered development changes.
This is our backbone where all the different fix and new feature are mixed with each other.

![image alt text](/assets/images/docs/scm/develop-branch.png =1000x)

### Actions

#### Merge Develop to Master Branch

*Release process applies on master*

**When:** After FQA/TQA perform regression test on Develop Branch. VPs give a GO.

**Who:** PLF Team with support of team responsible of each project

**How:**
{% highlight sh %}
git checkout develop
git pull
git checkout master
git pull
git merge --no-ff develop
git push
{% endhighlight %}

## Feature Branch

```Engineering```

Feature branches are dedicated branch to develop a new feature.

![image alt text](/assets/images/docs/scm/feature-branch.png =300x)

### Actions

#### Create a new Feature Branch

**When:** A new feature is specified and planified.

**Who:** PL/TL

**How:**

If you want the branch deploy on Acceptance, do not create the branch by yourself but create a SWF ticket on Jira for the full package (Branches+CI+Acceptance). 

If it’s a local feature project without need for CI or Acceptance you can create it by yourself.

#### Rebase Develop to Feature Branch

**When:** Frequently

**Who:** Team responsible of the branch with support of team responsible each project.

**How:**
{% highlight sh %}
git checkout develop
git pull
git checkout feature/x
git rebase develop
git push --force
{% endhighlight %}

#### Merge Feature Branch to Develop

**When:** Feature has been successfully tested by FQA. VPs give a GO.

**Who:** Team responsible of the branch with support of team responsible of each project

**How:**
{% highlight sh %}
git checkout feature/x
git rebase -i origin/develop
(remove initial commit)
git checkout develop
git pull
git merge --no-ff feature/x
git push
{% endhighlight %}

#### Remove a Feature Branch

**When:** Just after the merge of the feature branch to Develop

**Who:** PL/TL

**How:**

Create SWF ticket on Jira to remove the full package (Branches+CI+Acceptance).

## Fix Branch

```Engineering / GSS```

Fix Branch are dedicated branch to fix a bug. The validation process may be different if the bug has been raised by FQA/TQA or by SM.

A fix branch is always created from Develop branch (except exceptional circumstance: fix on stable only).

![image alt text](/assets/images/docs/scm/fix-branch.png =400x)

### Actions

#### Create a Fix Branch

**When:** A Jira issue has been created, time to resolve it is already estimated.

**Who:** Team responsible to fix the issue.

**How:**
{% highlight sh %}
git checkout develop
git pull
git checkout -b fix/issue
git push
{% endhighlight %}

#### Merge a Fix Branch to Develop

**When:**

* If issue raised by TQA/FQA: After Engineering test
* If issue raised by SM: After SM test

**Who:**

* If issue raised by TQA/FQA: Team responsible to fix the issue
* If issue raised by SM: SM 

**How:**
{% highlight sh %}
git checkout fix/issue
git pull
git rebase origin/develop
git checkout develop
git pull
git merge fix/issue --squash
git commit -a
git push
{% endhighlight %}

#### Remove a Fix Branch

**When:** After the merge of the fix branch to Develop

**Who:** Team responsible to fix the issue.

**How:**
{% highlight sh %}
git push origin --delete fix/issue
git branch -d fix/issue
{% endhighlight %}

## Stable Branch

```GSS```

Stable branch are used to perform releases and write / accept fix.

![image alt text](/assets/images/docs/scm/stable-branch.png =800x)

### Actions

#### Create a new Stable Branch

**When:** When create the first Release Candidate version

**Who:** SWF

**How:**

With a script similar to [https://github.com/exoplatform/swf-scripts/blob/master/createFB.sh](https://github.com/exoplatform/swf-scripts/blob/master/createFB.sh)

#### Create a Fix Branch to fix Stable Branch

**In exceptional circumstance**

**When:** A fix need to be done on a specific version but not on the on development version (fix a performance issue for instance) 

**Who:** Team responsible to fix the issue after a Go from SM.

**How:**
{% highlight sh %}
git checkout stable/4.1.x
git pull
git checkout -b fix/4.1.x-issue
{% endhighlight %}

#### Merge a Fix Branch to Stable

**In exceptional circumstance**

**When:** After SM test

**Who:** SM Team

**How:**
{% highlight sh %}
git checkout fix/4.1.x-issue
git checkout stable/4.1.x
git pull
git merge fix/4.1.x-issue --squash
git commit -a
git push
{% endhighlight %}

#### Remove a Fix Branch

**When:** After the merge of the fix branch to stable branch

**Who:** SM

**How:**
{% highlight sh %}
git push origin --delete fix/4.1.x-issue
git branch -d fix/4.1.x-issue
{% endhighlight %}

#### Perform a release

**When:** After FQA/TQA test campaign. VPs give a GO.

**Who:** Release managers

**How:**
{% highlight sh %}
git clone git@github.com:exoplatform/xxx.git
cd xxx
# You checkout the release branch on which you need to perform a release.
git checkout stable/A.B.x
# You follow the classical maven release process
mvn release:prepare
mvn release:perform
{% endhighlight %}

#### Move a release tag

**In really special case** (when the test campaign show a critical issue after tagging but before nexus publishing) release manager still can apply a last minute commit and move the tag.

**When:** After FQA/TQA test campaign. VPs give a GO.

**Who:** Release managers

**How:**
{% highlight sh %}
# After your commit, just delete the remote tag, and create another one in this way
git tag -d 1.0.0
git push origin :refs/tags/1.0.0
git tag 1.0.0
git push origin 1.0.0
{% endhighlight %}

## Integration Branch

```Engineering```

Integration branches are dedicated branch to automatic integration task (like Crowdin translation for instance).

![image alt text](/assets/images/docs/scm/integration-branch.png =1000x)

### Actions

#### Create a new Integration Branch

**When:** After a PLF release for Translation branches.

**Who:** SWF

**How:** Create from develop or stable/4.1.x. These branches have no maven version updated. Everything is done in a megabuild like for master build.

## PoC Branch

```Engineering```

Poc branches are dedicated branch to develop a Prove of Concept (PoC).

![image alt text](/assets/images/docs/scm/poc-branch.png =300x)

### Actions

#### Create a new PoC Branch

**When:** A new PoC is planified.

**Who:** PL/TL

**How:**
{% highlight sh %}
git checkout develop
git pull
git checkout -b PoC/x
[Modify all pom: initial commit]
git add pom.xml
git commit -m "details"
git push
{% endhighlight %}

## Improvement

### What is changing compare to 4.1

* Clean history by using git rebase.
* No more weekly merge between develop and master.
* All fixes are push firstly to develop branch. Then SM backport what they need to stable.
* Rebase develop to feature branch:
    * To do it regularly
    * To do it ONLY if develop branch is ok : build + acceptance are ok otherwise you'll distribute shitty code everywhere
    * To do it for all projects in a given FB at the same time (to keep the coherency)
* No more master branch on exodev repository. Master is only on blessed repository.
