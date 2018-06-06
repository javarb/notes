# notes

## Session 01/06/2018

- Introduction to the Java boilerplate
- Basic use of classes and objects and datatypes 
- Highlight the importance of test our code 
- Enum method example 
- Git & GitHub basics 
- Use Markdown notes

### Suggested lectures:

* [Law of Demeter](https://en.wikipedia.org/wiki/Law_of_Demeter)
* [Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)

## Session 04/06/2018
- Fork databasic project from github.com/kinbiko repo and clone locally
- Write the databasic requirements
- Write databasic design
- Initializate Java IntellyJ IDEA project into the cloned directory and commit changes

### Notes:
-  Design is very important, in desing we just put the strategy to follow not implentation details, indeed the Software engineers are 
problem solvers so if a problem arise we have to make more design before to go to code.

- For this design stage of the project we have to consider what kind of operations we are going to be using into our main Java method.
These are Insert and Query

- There is two ways to return to a previous state in Git 
	- _'[git revert](https://www.atlassian.com/git/tutorials/undoing-changes/git-revert)'_ allows to undo changes made to an specific commit making one new just "inverted": Delete the added and add the deleted.

	- _'[git reset](https://www.atlassian.com/git/tutorials/undoing-changes/git-reset)'_ undo commits making HEAD and master to point to an specific commit and discarding the others (deletes the history)

- When is necessary to correct some commit, use:
```git
git add <exp>
git commit -m '<commit_text>' --amend
git push -f
```
Where `<commit_text>` is the commit to be corrected and `<exp>` is a file or a regular expression to match.

**Be carefully** because this overwrite the previous commit. So non `git reset` or `git revert` will work. This means thereis a loose data risk.

### Suggested lectures:
* [RFC-3999](https://www.ietf.org/rfc/rfc3339.txt) (Datetime standard)
* [Agile Manifesto](http://agilemanifesto.org/)
* [GIT reset, revert, checkout](https://www.atlassian.com/git/tutorials/resetting-checking-out-and-reverting)
* [Dijkstra's algorithm](https://en.wikipedia.org/wiki/Dijkstra%27s_algorithm) (About interview problems)

### Homework
- Design query and write design code in Java (input and query).
