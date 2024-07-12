# Git Commands

# Git log

Shows all of the commits of a repo

```sh
$ git log
```
![image](https://github.com/jestebanzapata/gitPractice/assets/1307874/47d8c044-7da9-4923-b779-269f84d9f322)

You can even specify the branch name in order to see the logs of an specified branch or use the --oneline argument to see the logs in one like this (and easier way to read the commits):

```sh
$ git log <BRANCH_NAME> --oneline
```
![image](https://github.com/jestebanzapata/gitPractice/assets/1307874/2118b8fb-1709-4fa8-a2e3-3ed02448ab87)


## Git Diff

This is a command that show us the difference between commits, branches, files and more. 

```sh
$ git diff <COMMIT>
```


## Git Reset

We use this command to undo commits that have not benn pushed to a remote repository. There are two main options to use with this command:

`git reset --soft <COMMIT>` 
`git reset --hard <COMMIT>`


### Git reset --soft

```sh
$ git reset --soft <COMMIT>
```

This command will move back to the specified commit, it will remove all of the commits after the specified commit but it will preserve the changes. In other words it will only remove the changes from the staging area.

You can even use the HEAD to specify how many commits you want to reset, <N> is the numbers of commits: 

```sh
$ git reset --soft HEAD~<N>
```

### Git reset --hard

```sh
$ git reset --hard <COMMIT>
```

This command will move back to the specified commit, Any changes to tracked files in the working tree since <COMMIT> are discarded. This is a `dangerous command`, if you dont take care you can remove things that you don't want:

You can even use the HEAD to specify how many commits you want to reset, <N> is the numbers of commits: 

```sh
$ git reset --hard HEAD~<N>
```

## Git Revert

This command is kind of similar to the reset command but it behaves different, to use this command you do something like:

```sh
$ git revert <COMMIT_TO_REVERT>
```
It creates a new commit that revert changes based only in the commit you want to revert, it does not remove any of the commits.


## Git merge

This command combine two o more branches in the current branch

```sh
$ git merge main
```
![01 Branch-2 kopiera](https://github.com/user-attachments/assets/ca81f0a4-5112-4654-9f59-99354258d7f7)

## Git rebase

This command will move the totality of a branch into another point of the branch

![image](https://github.com/user-attachments/assets/b798969c-2b05-47a1-8b78-83fcee574346)

Suppose we are in the branch called `Feature`, this branch has two commits but our base is pointing out to a past commit, in order to keep a linear history we can use rebase to point to the HEAD of the main branch.

```sh
$ git rebase main
```

Later we can go back to our main branch and use the 4rebase command again to merge these new commits in the main branch

```sh
$ git checkout main
$ git rebase Feature
```

Reabse command should not be used with public branches, due that this command rewrites history and it someones is doing changes there, they will be affected because the commits are not going to match.

## Git cherry pick

This commando takes the changes of the specified commits and apply these changes in a new commit in the working directory. Notes: This command will create a new commit with the changes.

```sh
$ git cherry-pick <COMMIT> <COMMIT>
```

In case there are conflicts we could use this command after resolving them:

```sh
$ git cherry-pick --continue
```
or abort the cherry picking action:
```sh
$ git cherry-pick --abort
```

### Cherry pick alternative

#### Git diff and git apply

you can save the differences between two commits, branches or files and use to difference to apply them in a new branch.
```sh
$ git diff <COMMIT> <COMMIT>
```
this will show the difference between two commits

![image](https://github.com/user-attachments/assets/43c1c198-1c24-4cf6-abec-c21895e3d279)

but you need to save these differences in a new file, in order to do that you need to define where you are going to save this info, like this:

```sh
$ git diff <COMMIT> <COMMIT> > <FILE_TO_SAVE_DIFF>
```
with the '>' you are redirecting the output of the git diff command to a file.

Now with the git apply command, you can read the supplied diff output and applies it to a file in our working directoy.

```sh
$ git apply <FILE_WITH_DIFF>
```
This commando applies the patch but it does not create a new commit. 

#### Checkout

you can use checkout command to take the changes of a file in a different branch and apply the changes in another branch.

E.g lets suposse that we are in the main branch

```sh
$ git checkout <BRANCH_NAME> -- <FILE_TO_USE>
```

with this we are taking the changes of the file <FILE_TO_USE> and apply them in the same file that we have in the main branch.


