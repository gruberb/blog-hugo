+++
categories = ["Coding"]
description = ""
tags = ["coding"]
date = "2017-05-04T18:37:04+02:00"
title = "Git proficiency with rebase"
+++

I am a developer now for more than 10 years. Except a few years with SVN, I was solely working with Git. The best quote I got from one of my CTOs in the early days, was:

"Git is like the whole world, but we need just the size of a lake of it."

You mainly use:

- git clone
- git pull
- git push
- git add
- git commit
- git checkout and git checkout -b

That's mostly it, right? Creating new branches, pushing them to Bitbucket or GitHub, and then merge them via the GUI of one of the two websites.

My latest project let me work with around 7 developers, and we all work on the same project, and on multiple GitHub issues at once. There, a simple "git merge develop MYBRANCH" didn't cut it anymore. More was needed. And there I found it, the holy command of the year 2017. At least of my version of 2017.

### "git rebase -i HEAD~3" and other funny things.

A colleague in the current project introduced me to a whole new world of telling "stories" with your git commits. Grouping them together so the reviewer gets a sense of what is going on and for which reason. Back then, in the old days, I would just commit around 10 times, push it all to GitHub and the reviewer went file for file and try to understand what's going now.

Now though, I group commits together which belong together. So the reviewer can go commit by commit through my pull request and understand what's going on.

### An example

I mainly work with React in the frontend is the current project, so lets grab an issue from GitHub which is called "Add a switch component to the User registration form". The steps we will complete the task is:

- First find if an existing switch component exists
- Grab the component and place it inside the existing form
- Figure out we need to adjust the css slightly to make it work
- Test the switch by hand in the browser
- If everything works, we are happy and commit
- Afterwards we realise we cannot use the return value of the Switch component (it's on/off instead of true/false)
- Therefore we rewrite the logic of the Switch
- We wire the new switch with the existing user form logic
- We test it, it works, we commit
- We run the tests and figure out some old tests fail
- We rewrite the tests, change some more logic, and commit
- Now the linting fails, so we fix some idention issues and add missing semicolons
- We commit and are done.

So we have around 3-4 commit with this pull request, everything is mixed up and from the timing of the commits and the grouping of the resulting code, it's really hard to read. So here it comes, our rescue:

### git rebase -i HEAD~4

Before we move on, we have to make sure that our current "develop" branch is up to date. Therefore we:

- `git checkout develop`
- `git pull`

(`git pull` works differently then `git pull origin develop`. With `git pull`, we'll get the whole history of every branch, also from the remote ones.)

and then, checkout our feature branch again:

- `git checkout 1234-switch-userform`

And now comes the magic. We can group different commits together with the use of `git rebase -i HEAD~4`. 


