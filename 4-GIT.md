# ICCS474
## Internet Programming

### GIT

Git is a distributed version control system that allows multiple developers to work on specific project independently.

Write your own note, it is very important that your remember these commands

Commands reference from Live example.
```bash
git init
git status
git add .
git commit -am '<MESSAGE>'
git branch <BRANCHNAME>
git checkout <BRANCHNAME>
git merge <BRANCHNAME>
git remote -v
git remote add origin <GIT URL>
git remote remove origin <GIT URL>
git push
git pull
git clone <GIT URL> <TARGET PATH>
```

### Basic Branching

![Image](https://raw.githubusercontent.com/SaKKo/muic-iccs474-2015t2/master/assets/git-branch.png)

### Exercise

1. Clone https://github.com/SaKKo/muic-iccs474-2015t2-exercise1
1. What is fibonacci?
1. Check code performance.
    1. How to improve?
1. There are 3 branches, `master` `memoize` `memoizer`
    1. We will use Memoize Pattern
    1. See the differences.
    1. Is it really faster?
    1. Merge `memoize` to master
    1. Merge `master` to `memomizer`
        1. fix conflicts
    1. Merge `memoizer` to `master`
1. Move to your own GIT
    1. Create your own repository in github or bitbucket
    1. run `git remote add myorigin <GitURL>`
        1. the default is `origin`
        1. you can see how many `remote` are there by running `git remote -v`
    1. run `git push myorigin master`
        1. check github if the code is updated.
1. Try removing `sakko` from default `origin`
    1. hint `git remote remove <OriginName>`
1. Try moving `myorigin` to `origin`
1. Try pushing and see if it works.
1. Try inviting your friends to your repositories.
    1. Give them write permission in Github
    1. Ask your friend to modify your repository.
        1. just add any code and `git push`.
        1. Figure out how to merge it.
            1. hint you must do `git pull` first so that your local repo is updated to the same state as github.

### Ruby

We've learned a few ruby syntax today. We will be using it quite a lot. You might want to read more about its basic syntax.

This is one great online tutorial.
https://www.codeschool.com/courses/try-ruby

Just like python, you can start ruby shell by running `irb` in terminal. Then you can start writing ruby code there.
