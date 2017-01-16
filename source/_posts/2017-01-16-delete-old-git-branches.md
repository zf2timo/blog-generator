---
title: Delete old git branches
tags: [git, tip]
categories: [development]
---
#Delete old git branches

When working with git you <s>should</s> have to use branches. But over the time, there will be a lot of branches that
arn't needed anymore.

To get rid of this waste, i created a script to delete them:
```bash
#!/usr/bin/env bash

BRANCHES="$(git branch --merged | grep -v "\*" | grep -v "master" | grep -v "develop")"

if [ -z $BRANCHES ]; then
    echo "No branch can deleted safely"
    exit 1;
fi

echo "The following branches will be deleted:"
echo $BRANCHES
echo "Are you sure? (y or n)"
read ANSWER

if [ $ANSWER = "y" ]; then
    echo $BRANCHES | xargs -n 1 git branch -d
fi
```
It selects all branches which are merged into master branch and after a confirmation, they will be deleted.