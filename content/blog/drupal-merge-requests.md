+++
author = "Greg Boggs"
categories = ["Drupal"]
date = "2020-11-20"
draft = false
tags = ["Drupal"]
title = "Drupal Merge Requests using Gitlab!"
url = "/drupal-merge-requests/"
[menu.featured]

+++
Drupal.org has used patches to manage community contribution for many years. But, patches are difficult for new users to learn and require the use of the command line. Recently, Drupal.org code has migrated to Gitlab, and we can now use Gitlab and Drupal.org issues to create Merge Requests to share code and fixes with modules and Drupal Core. Here's an [overview of creating a merge request](https://www.drupal.org/docs/develop/git/using-git-to-contribute-to-drupal/creating-issue-forks-and-merge-requests) for folks who want all the details.

## Drupal Forks are Special

Drupal Gitlab forks are special because they are accessible to everyone with a Drupal.org account. One fork per issue, and anyone can edit the fork and open a merge request to the main project.

## Setup your Drupal Account

Before we begin, you must register for an account on Drupal.org to get access to gitlab forks. Next, add an [ssh public key to your Drupal.org user profile](https://www.drupal.org/drupalorg/docs/user-accounts/git-authentication-for-drupalorg-projects) so you don't need a password to work. Lastly, agree to the Drupal.org [git terms of service so you can access forks](https://www.drupal.org/docs/develop/git/setting-up-git-for-drupal/obtaining-git-access).

## Create an issue on Easy Breadcrumb

Before you can create forks on Drupal.org's gitlab, you need an issue! So, start by [creating an issue on Easy Breadcrumb](https://www.drupal.org/node/add/project-issue/easy_breadcrumb).

Once you have the issue, press "Create issue fork".

## Clone Easy Breadcrumb

Next copy of the module you want to modify. You can get instructions for this by clicking [version control](https://www.drupal.org/project/easy_breadcrumb/git-instructions) near the top of the module.

```
git clone --branch 8.x-1.x git@git.drupal.org:project/easy_breadcrumb.git
cd easy_breadcrumb
```

## Make Your Changes

Now, edit the code on your own computer to fix the issue. This is the hardest part!

## Send Your Work to the Issue Fork on Gitlab

The exact git commands vary slightly from issue to issue. So, check the "view commands" link on the issue to see the commands for your issue, but here are the ones I ran. I got the commit message from the commit credit section towards the bottom of the issue.

```
git remote add easy_breadcrumb-3174165 git@git.drupal.org:issue/easy_breadcrumb-3174165.git
git fetch easy_breadcrumb-3174165
git checkout -b '8.x-1.x' --track easy_breadcrumb-3174165/'8.x-1.x'
git add .
git commit -m 'Issue #3174165 by kell.mcnaughton, pattsai: How to support limiting depth' --author="git <git@3602480.no-reply.drupal.org>"
git push --set-upstream easy_breadcrumb-3174165 HEAD
```


The commands do the following:

* Add the new fork as a remote.
* Fetch the new fork.
* Checkout a branch on that fork.
* Add your work to that branch.
* Commit your work to that branch.
* Push your work to Gitlab.

## Open a Merge Request

Once your work is saved to the issue fork on Gitlab. Go back to the issue on Drupal.org and click Compare near the top of the issue. Then, click open merge request!

Now that your request is open, the maintainer of the module just needs to press merge on Gitlab to make the code part of the project!
