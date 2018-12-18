# SOFTWARE ENGINEERING IN JAVA

## Session 19 (04/12/2018)

- Testing to http endpoints

### Notes:

####

Cloned the roger code in https://github.com/kinbiko/talenthaven-api

Explained concepts

his code was to have a generic test to http endpoints to whatever HTTP verb used

###  Homework

Deploy dependencies in docker-compose.yml in talenthaven-api

in js homewokr previous session the fronted has to show in text, this can be achieved using some library but the most simple
is to return an JSOn object in the API that has a text with the number and then use in the frontend.

some popular frontend libraries that have all embeeded are react and angular

https://github.com/facebook/create-react-app


About the {} being prefereable than [], this was (apart the security reason) because if we need to change or add something to
  our response will be easier if we have an object instead an array, if I have an array and want to return another thing, I'll have make a new object
  and add that new thing anyway

---
[jaar@port-staff Java-programming]$ mv calculator-frontend/ calculator-frontend.old
[jaar@port-staff Java-programming]$ git clone git@github.com:javarb/calculator-frontend.git
[jaar@port-staff Java-programming]$ cd calculator-frontend
[jaar@port-staff calculator-frontend]$ git branch -a
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/delete-me-after-review
  remotes/origin/frontend-bs4
  remotes/origin/master
[jaar@port-staff calculator-frontend]$ git checkout remotes/origin/delete-me-after-review
Note: checking out 'remotes/origin/delete-me-after-review'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by performing another checkout.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -b with the checkout command again. Example:

  git checkout -b <new-branch-name>

HEAD is now at 66023c8 Empty repo for reviewing purposes

[jaar@port-staff calculator-frontend]$ git branch
* (HEAD detached at origin/delete-me-after-review)
  master
[jaar@port-staff calculator-frontend]$ ls

nothing there

[jaar@port-staff calculator-frontend]$ git branch -a
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/delete-me-after-review
  remotes/origin/frontend-bs4
  remotes/origin/master
[jaar@port-staff calculator-frontend]$ git checkout frontend-bs4
Branch 'frontend-bs4' set up to track remote branch 'frontend-bs4' from 'origin'.
Switched to a new branch 'frontend-bs4'
[jaar@port-staff calculator-frontend]$ ls
index.html  public
[jaar@port-staff calculator-frontend]$ git branch
* frontend-bs4
  master


- Preguntar:
  - In https://github.com/javarb/calculator-frontend/pull/2 this has merged to delete-me-after-review branch and now is ahead than master
    What I should to do? solved
  - Conflict en https://github.com/javarb/api/pull/4 why?
  - Just the String -> POJO change we discussed last session (https://github.com/javarb/api/pull/5).
    I merged this branch `bugsnag-integration` but I added other change, so I have to make PR again? or should I revert merge and merge again?

    I want to work on from the version that has the bug solved (but is in conflict) , to make improvements (return a JSON) and to add a new branch with the HTTP endpoint methods tests

### Resources:
- [][1]

[1]:
