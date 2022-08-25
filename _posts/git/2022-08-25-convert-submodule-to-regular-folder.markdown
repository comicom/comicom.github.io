---
layout: posts
title:  "How to convert submodule to regular folder"
date:   2022-08-13 12:10:28 +0900
categories: git
tags:
  - git
---
{% highlight shell %}
# Fetch the submodule commits into the main repository
git remote add submodule_origin git://url/to/submodule/origin
git fetch submodule_origin

# Start a fake merge (won't change any files, won't commit anything)
git merge -s ours --no-commit submodule_origin/master

# Do the same as in the first solution
git rm --cached submodule_path # delete reference to submodule HEAD
git rm .gitmodules             # if you have more than one submodules,
                               # you need to edit this file instead of deleting!
rm -rf submodule_path/.git     # make sure you have backup!!
git add submodule_path         # will add files instead of commit reference

# Commit and cleanup
git commit -m "removed submodule"
git remote rm submodule_origin
{% endhighlight %}