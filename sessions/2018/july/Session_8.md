# SOFTWARE ENGINEERING IN JAVA

## Session 8 (24/07/2018) (*working on*)

There was a GitHub's pull request for session 5 but as the time was passing, changes in the session 6 and 7 were added. This request had several commits in the same pull request and this is not a good practice, this would be better to have each pull request for a particular session. Also, its recommended that a pull request have less than 500 files per pull request solicitude.

In order to do this, a branch must be created for each session and after generate a pull request for each one, and once each pull request be approved, merge to master.

So, in order to fix the issue of have several commits in the same pull request, we had to create 2 branches. The first branch should to contain what was reviewed still that moment by Roger, and the other branch the session 7 content. The idea behind this was to make a pull request for each content, and this idea is extended in ahead for each session. This means, a branch should be created for session 8 and a pull request open in order to merge this branch into master once the pull request be accepted.

Following the changes that were made in order to achieve this.

The first thing we had to make was to get the desired commit id:

```bash
[jaar@port-staff notes]$ git log --oneline
dcbb20a (HEAD -> master, origin/master, origin/HEAD) Merge corrections
e7b5097 Merge corrections
eac52c5 Added Session 7
fea3185 Updated TODOS
e892ef0 some updates
d8dc181 Added session 6 content
413c4f5 Updates to session 5
d7549fd Created Session 6 file
05d4ba1 Updated Session 5
3efe033 Updates to session 5
49a5301 Updated session 5
3fcea34 Changes in Session 5
d4e5719 Updated requested changes PR Session 4
...
```

In order to make `HEAD` to point to that commit (`3fcea34 Changes in Session 5`), we used the following command:

```bash
[jaar@port-staff notes]$ git checkout 3fcea34
Note: checking out '3fcea34'.

You are in 'detached HEAD' state. You can look around, make experimental changes and commit them, and you can discard any commits you make in this state without impacting any branches by performing another checkout.

If you want to create a new branch to retain commits you create, you may do so (now or later) by using -b with the checkout command again. Example:

  git checkout -b <new-branch-name>

HEAD is now at 3fcea34... Changes in Session 5
```
Now, from that point in history we created a new branch in order to put there the content Roger had reviewed still that moment (sessions 5 and 6):

```bash
[jaar@port-staff notes]$ git checkout -b session-5-and-6
Switched to a new branch 'session-5-and-6'
```

If we tried to do `git push` we found an error because in GitHub that branch doesn't existed yet.

```bash
[jaar@port-staff notes]$ git push
fatal: The current branch session-5-and-6 has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin session-5-and-6
```

For that, in order of create that remote branch ans sync with the local we executed:

```bash
[jaar@port-staff notes]$ git push --set-upstream origin session-5-and-6
Total 0 (delta 0), reused 0 (delta 0)
To github.com:javarb/notes.git
 * [new branch]      session-5-and-6 -> session-5-and-6
Branch session-5-and-6 set up to track remote branch session-5-and-6 from origin.
```

In this point was neccesary to copy all the raw content of the last commit from the `master` branch of my repo in GitHub, which had the changes still the pull request with all those changes, and put into the corresponding files in the local branch. That in order of simulate what we should have done from beginning: make changes in the corresponding branches and not in `master`.

So files were updated, commited and pushed to the remote branch:

```bash
[jaar@port-staff notes]$ git add sessions/2018/july/Session6.md ; git commit -m 'Session 6 added'; git push
[session-5-and-6 126ab46] Session 6 added
 1 file changed, 352 insertions(+)
 create mode 100644 sessions/2018/july/Session6.md
Counting objects: 6, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (4/4), done.
Writing objects: 100% (6/6), 3.99 KiB | 0 bytes/s, done.
Total 6 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To github.com:javarb/notes.git
   3fcea34..126ab46  session-5-and-6 -> session-5-and-6

[jaar@port-staff notes]$ git add sessions/2018/june/Session_5.md ; git commit -m 'Session 5 added'; git push
[session-5-and-6 e80a04d] Session 5 added
 1 file changed, 155 insertions(+), 5 deletions(-)
Counting objects: 6, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (5/5), done.
Writing objects: 100% (6/6), 4.26 KiB | 0 bytes/s, done.
Total 6 (delta 2), reused 0 (delta 0)
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
To github.com:javarb/notes.git
   126ab46..e80a04d  session-5-and-6 -> session-5-and-6
```

Now we can see how in the log how from the point we began, we have the last two commits above:

```bash
[jaar@port-staff notes]$ git log --oneline
e80a04d (HEAD -> session-5-and-6, origin/session-5-and-6) Session 5 added
126ab46 Session 6 added
3fcea34 Changes in Session 5
...
```

And we made the same for the content of the session 7 by creating a new branch from the branch we are currently on which is `session-5-and-6`:
```bash
[jaar@port-staff notes]$ git checkout -b session-7
Switched to a new branch 'session-7'
```

We also setted and push the upstream branch:
```bash
[jaar@port-staff notes]$ git push --set-upstream origin session-7
Total 0 (delta 0), reused 0 (delta 0)
To github.com:javarb/notes.git
 * [new branch]      session-7 -> session-7
Branch session-7 set up to track remote branch session-7 from origin.
```

Now, there was something happend, that I made a typo of the session 6 file:

```bash
[jaar@port-staff notes]$ cd sessions/2018/july/
[jaar@port-staff july]$ ls
Session6.md  Session_7.md
```

In order to solve this, we just have to rename:

```bash
[jaar@port-staff july]$ mv Session6.md Session_6.md
```
```
If we execute`git status` we can see these changes ocurring:

```bash
[jaar@port-staff july]$ cd -
/home/jaar/Git/GitHub/Java-programming/notes

[jaar@port-staff notes]$ git status
On branch session-7
Your branch is up-to-date with 'origin/session-7'.
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        deleted:    sessions/2018/july/Session6.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        sessions/2018/july/Session_6.md
        sessions/2018/july/Session_7.md

no changes added to commit (use "git add" and/or "git commit -a")
```

Then, when we add this new file that needs to be commited, Git can interpretate that we only changed the name:

```bash
[jaar@port-staff notes]$ git add sessions/2018/july/Session6.md sessions/2018/july/Session_6.md

[jaar@port-staff notes]$ git status
On branch session-7
Your branch is up-to-date with 'origin/session-7'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        renamed:    sessions/2018/july/Session6.md -> sessions/2018/july/Session_6.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        sessions/2018/july/Session_7.md
```

So as this was updated we commit changes:

```bash
[jaar@port-staff notes]$ git commit -m 'rename Session 6'; git push
[session-7 f9d2a06] rename Session 6
 1 file changed, 0 insertions(+), 0 deletions(-)
 rename sessions/2018/july/{Session6.md => Session_6.md} (100%)
Counting objects: 5, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (5/5), 410 bytes | 0 bytes/s, done.
Total 5 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To github.com:javarb/notes.git
   e80a04d..f9d2a06  session-7 -> session-7
```

After, we made the correspondent changes into session 7 file using my GitHub master branch raw content:

```bash
[jaar@port-staff notes]$ git add sessions/2018/july/Session_7.md ; git commit  -m 'Added Session 7'; git push
[session-7 e96b972] Added Session 7
...
To github.com:javarb/notes.git
   f9d2a06..e96b972  session-7 -> session-7
```
NOw, in order to clean orur master, we had to delete it: **This is very dangerous** and only must be done if we are sure what we are doing. In this case is okay since after the two branches were pushed, two pull requests were made and Roger was updating his master branch, so we are going to create our branch form his master branch.

So, first to do is to stand again in our selected base commit:

```bash
[jaar@port-staff notes]$ git checkout 3fcea34
Note: checking out '3fcea34'.
...
HEAD is now at 3fcea34... Changes in Session 5
```

Now we see we are again in our base commit `3fcea34 (HEAD) Changes in Session 5`:

```bash
[jaar@port-staff notes]$ git log --oneline
3fcea34 (HEAD) Changes in Session 5
d4e5719 Updated requested changes PR Session 4
```

If I want to see the branches I have:

```bash
[jaar@port-staff notes]$ git branch
* (HEAD detached at 3fcea34)
  master
  session-5-and-6
  session-7
```

We were `dettached` from a specific branch and so we were able tp delete our master branch:

```bash
[jaar@port-staff notes]$ git branch -d master
warning: deleting branch 'master' that has been merged to
         'refs/remotes/origin/master', but not yet merged to HEAD.
Deleted branch master (was dcbb20a).
```

Aftet it, we recreate the `master` branch

```bash
[jaar@port-staff notes]$ git checkout -b  master
Switched to a new branch 'master'
```

And we setted the upstream channel:

```bash
[jaar@port-staff notes]$ git push
fatal: The current branch master has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin master

[jaar@port-staff notes]$ git push --set-upstream origin master
To github.com:javarb/notes.git
 ! [rejected]        master -> master (non-fast-forward)
error: failed to push some refs to 'git@github.com:javarb/notes.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

As we can see in the beginning there were errors because master remotely had another content, but anyway we force it because we knew what we wanted with it:

```bash
[jaar@port-staff notes]$ git push --set-upstream origin master -f
Total 0 (delta 0), reused 0 (delta 0)
To github.com:javarb/notes.git
 + dcbb20a...3fcea34 master -> master (forced update)
Branch master set up to track remote branch master from origin.
```

Finally, we create the branch for this session:

```bash
[jaar@port-staff notes]$ git checkout -b session-8
Switched to a new branch 'session-8'
```

And `push` creating the upstream:

```bash
[jaar@port-staff notes]$ git push
fatal: The current branch session-8 has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin session-8

[jaar@port-staff notes]$ git push --set-upstream origin session-8
Total 0 (delta 0), reused 0 (delta 0)
To github.com:javarb/notes.git
 * [new branch]      session-8 -> session-8
Branch session-8 set up to track remote branch session-8 from origin.
```

And finally, as we are in the commit `3fcea34 (HEAD) Changes in Session 5`, there wer haven't *july* month created, so we have to do this directory:

[jaar@port-staff notes]$ mkdir sessions/2018/july
[jaar@port-staff notes]$ touch sessions/2018/july/Session_8.md

I think here is an error in create the branch for session 8 since this should have been created from session 7 changes, in order includes the last changes still the moment, and now this was created over a commit very outdated.1 **Pendiente cambiar!**


```bash
[jaar@port-staff july]$ ls
Session_8.md
```

```bash
[jaar@port-staff july]$ git log --oneline
3fcea34 (HEAD -> session-8, origin/session-8, origin/master, origin/HEAD, master) Changes in Session 5
...
```

```bash
[jaar@port-staff july]$ git branch
  master
  session-5-and-6
  session-7
* session-8
```

```bash
[jaar@port-staff july]$ git checkout -m session-7
Switched to branch 'session-7'
Your branch is up to date with 'origin/session-7'.
```

```bash
[jaar@port-staff july]$ git branch
  master
  session-5-and-6
* session-7
  session-8
[jaar@port-staff july]$ ls
Session_6.md  Session_7.md  Session_8.md
[jaar@port-staff july]$ git log --oneline
e96b972 (HEAD -> session-7, origin/session-7) Added Session 7
f9d2a06 rename Session 6
e80a04d (origin/session-5-and-6, session-5-and-6) Session 5 added
126ab46 Session 6 added
3fcea34 (origin/session-8, origin/master, origin/HEAD, session-8, master) Changes in Session 5
...
```

```bash
[jaar@port-staff july]$ git checkout session-8
Switched to branch 'session-8'

Your branch is up to date with 'origin/session-8'.
[jaar@port-staff july]$ ls
Session_8.md
```

```bash
[jaar@port-staff july]$ git checkout session-7
Switched to branch 'session-7'
Your branch is up to date with 'origin/session-7'.

[jaar@port-staff july]$ ls
Session_6.md  Session_7.md  Session_8.md
```

[jaar@port-staff july]$ git branch
  master
  session-5-and-6
* session-7
  session-8
[jaar@port-staff july]$ git branch -d session-8
Deleted branch session-8 (was 3fcea34).

[jaar@port-staff july]$ ls
Session_6.md  Session_7.md  Session_8.md

[jaar@port-staff july]$ rm Session_8.md

[jaar@port-staff july]$ ls
Session_6.md  Session_7.md

I did changes in suggested by Roger in [PR #4](https://github.com/kinbiko/notes/pull/4) and merged without problem in his master branch.

Now as I want to merge into my master, I am seeing this message into my session-7 branch nto gitHub:

*This branch is 3 commits ahead, 3 commits behind master.*

And in the master ROger's branch says:

*This branch is 4 commits ahead, 1 commit behind javarb:master.*

I am going to merge my own changes into my master branch in GitHub, I do this in [this PR](https://github.com/javarb/notes/pull/3)

After that In GitHub branch *session-7* was deleted and also *session-5-and-6* (already merged) and *session-8* since I will recreate it again.

[jaar@port-staff july]$ git branch
  master
  session-5-and-6
* session-7
*
[jaar@port-staff july]$ git checkout master
Switched to branch 'master'
Your branch is up to date with 'origin/master'

[jaar@port-staff notes]$ git log --oneline
3fcea34 (HEAD -> master, origin/session-8, origin/master, origin/HEAD) Changes in Session 5
...

[jaar@port-staff notes]$ git pull
remote: Counting objects: 4, done.
...

[jaar@port-staff notes]$ git log --oneline
df50e8e (HEAD -> master, origin/master, origin/HEAD) Merge pull request #3 from javarb/session-7
e327814 (origin/session-7, session-7) Minor changes
72d74a3 Merge pull request #2 from kinbiko/master
e96b972 Added Session 7
f9d2a06 rename Session 6
f31033e Merge pull request #3 from javarb/session-5-and-6
e80a04d (origin/session-5-and-6, session-5-and-6) Session 5 added
126ab46 Session 6 added
5dde3c7 Merge pull request #1 from javarb/master
3fcea34 (origin/session-8) Changes in Session 5


[jaar@port-staff notes]$ git status
On branch master
Your branch is up to date with 'origin/master'.

nothing to commit, working tree clean

Trying to delete the local branches automatically
[jaar@port-staff notes]$ git branch
* master
  session-5-and-6
  session-7
[jaar@port-staff notes]$ git pull -p
From github.com:javarb/notes
 - [deleted]         (none)     -> origin/session-5-and-6
 - [deleted]         (none)     -> origin/session-7
 - [deleted]         (none)     -> origin/session-8
Already up to date.
[jaar@port-staff notes]$ git branch
* master
  session-5-and-6
  session-7

  [jaar@port-staff notes]$ git fetch origin --prune
  [jaar@port-staff notes]$ git branch
  * master
    session-5-and-6
    session-7

Finally I did it manually:

[jaar@port-staff notes]$ git branch -d session-5-and-6 session-7
Deleted branch session-5-and-6 (was e80a04d).
Deleted branch session-7 (was e327814).

[jaar@port-staff notes]$ git branch
* master
*
[jaar@port-staff notes]$ ls sessions/2018/july/
Session_6.md  Session_7.md

[jaar@port-staff notes]$ git checkout -b session-8
Switched to a new branch 'session-8'

[jaar@port-staff notes]$ ls sessions/2018/july/
Session_6.md  Session_7.md

[jaar@port-staff notes]$ cp ~jaar/Session_8.md sessions/2018/july/

[jaar@port-staff notes]$ git push --set-upstream origin session-8
Total 0 (delta 0), reused 0 (delta 0)
To github.com:javarb/notes.git
 * [new branch]      session-8 -> session-8
Branch 'session-8' set up to track remote branch 'session-8' from 'origin'.

and now the branch is sync in GitHub, but I have to make the commit:

[jaar@port-staff notes]$ git status
On branch session-8
Your branch is up to date with 'origin/session-8'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        sessions/2018/july/Session_8.md
...




**Working with Databasic**

Databasic was reviwed for cleaning code, so for example a method ended with few lines and for that this method was deleted and the lines placed (inline) into the calling method.

In order to convert a method in a inline statement we should use `ctrl+atl+n`.

Other significative change was that the query requirement was updated in README.md in order that the program required the string `query` in order to process one.

HOMEWORK

- [ ] Review code and change where this can be optimized, comments, logic. As good as I can
- [ ] Use `query` keyword
