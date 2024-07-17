# ***Git Commands & Notes***
Courtesy: **The Git & GitHub Bootcamp** - _Colt Steele_

---

### **Notes**

- `HEAD` refers to a branch reference and not a commit and the branch reference points to a commit
   - In detached HEAD, it refers to a commit hash


- [gitignore.io](https://www.toptal.com/developers/gitignore/) - it provides a general git ignore file for whatever 
   programing language we choose

- #### **Rewriting History** - to delete the previous commit
   - `git reset --hard HEAD~1`
   - `git push origin HEAD --force`

- #### **Travelling in time**

- `git checkout <commit_hash>/ HEAD~1/2/3`- moves in detached HEAD state
- `git switch <branch_name> OR git switch`- will re-attach the HEAD

- #### **git rebase vs git merge**

git merge preserves the history
git rebase re-writes the history
- `git merge <branch_name>`- merge `<branch_name>` into whatever branch you are in
- `git rebase -i HEAD~4` :- interactive rebase a series of commits onto the HEAD in the same branch


- #### [**GitHub pages**](https://pages.github.com/)
  - These public webpages thar are hosted and published via GitHub.
  - These are static webpages means just HTML/CSS/JS and does not support server-side code.
  - helpful for creating portfolio websites or documentation websites for your repositories.

  - `<gh-username>.github.io`- <u> user sites </u>: allowed one per GitHub account
  - `<gh-username>.github.io/repo-name`- <u> project sites </u>:

---

### **Commands**

#### [**git config**](https://git-scm.com/book/en/v2/Appendix-C%3A-Git-Commands-Setup-and-Config)

- `git config --global user.name`
- `git config user.name`- at the root level of project to override the default settings
- `git config --global user.email`
- `git config --local user.name` :- for local git config (within a repository)
- `git config --global core.editor "code --wait"`- to set VS Code as default editor
- `git config --global alias.s status` :- setting alias for git status. After configuring `git s` will be equivalent 
  to `git status`

Reference to [git aliases](https://github.com/GitAlias/gitalias) <br>
Some common aliases
> git a - git add <br>
> git b - git branch <br>
> git c - git commit <br>
> git d - git diff <br>

---

#### **git remote**

- `git remote add <remote_name> <url>`- standard name is origin, or we can give upstream
- `git remote rename <old> <new>`- to rename remote
- `git remote remove <name>`- to remove remote

---

#### **git add**

- `git add -A/--a`- stages all changes 
- `git add .`- stages new files and modifications, without deletions (on the current directory and its subdirectories). 
- `git add -u/--update` stages modifications and deletions, without new untracked files
- `git add -A` is equivalent to `git add .`;` git add -u`

---

#### **git log**

- `git log`- retrieves information which is a log of commits
- `git log --pretty=oneline,short,medium,full,fuller,reference,email,raw,foramt:<string> and tformat:<string>`
- `git log --oneline`

---

#### **git branch**
- To create new branches:
    - `git checkout -b <branch_name>`
    - `git switch -c <branch_name>`
- `git branch`- list of local branches
- `git branch -a`- list of all the branches (local & remote)
- `git branch -m <new_branch_name>`- to rename a branch
- `git branch -d <branch_name>`- to delete a branch if it has been pushed and merged with remote branch
- `git branch -D <branch_name>`- to force delete a branch even if it hasn't been pushed and merged with remote branch

---

#### **git diff**

- `git diff`- compares staging area and working directory (only shows the unstaged changes i.e not staged for next 
  commit)
- `git diff HEAD`- shows changes that are staged and unstaged since HEAD/last commit (HEAD is reference to last commit)
- `git diff --staged/--cached`- shows changes between the staging area and the last commit
- `git diff <branch_1>..<branch_2>`- list the change between the tips of branch 1 and 2
- `git diff <commit_1>..<commit_2>`- list the changes between 2 commits

---

#### **git push**

- `git push origin <local_branch>:<remote_branch>`- to push a different local branch to a different remote branch

---

#### **git fetch and pull**

- `git fetch <remote> <branch_name>`- branch name is optional, required only if we want to fetch only a particular 
  branch 
- `git pull`- combination of `git fetch` followed by `git merge`

---

#### **git stash**

- `git stash` or `git stash save` or `git stash -m`- to stash something
- `git stash list`- to list the stashes
- `git stash apply stash@{2}`-  to apply a stashed change
- `git stash drop stash@{2}`- to delete a stashed change
- `git stash pop stash@{2}`- combination of `git stash apply` and `git stash pop`
- `git stash clear`- to delete all the stashed changes

---

### **Discarding changes & Undoing commits**

#### git restore
- `git restore <file_name>` or `git checkout HEAD <file_name>` or `git checkout -- <file_name>`-after making a lot 
  of changes if I want to discard them then I just move back to HEAD
- `git restore --source HEAD~3 <file_name>`- to select different source, by default HEAD is the source
- `git restore --staged <file_name>`- to unstage a staged file

#### git reset
- `git reset <commit_hash>`- we move back to old commit but the changes we did will still be there in the working directory
- `git reset --hard <commit_hash>`- moves back to old commit but changes won't be there

#### git revert
- `git revert <commit_hash>`- it creates a new commit which undoes the latest commits which we did

#### **NOTE**: In `git reset` the history is lost but `git revert` saves the history

---

#### **git tags** - reference to a specific point in git history

- `git tag <tag_name>`- to create a tag
- `git tag` or `git tag -l`- list all the tags
- `git tag -l <some_wildcards>`- to view tags (filter tags with some wildcards) | ex:`git tag -l "*beta*"`
- `git diff <tag_1> <tag_2>`- to see the differences between the two tags
- `git tag -a <tag_name> -m "some message"`- to create an annotated tag
- `git show <tag_name>`- to see the details of the tag
- `git tag <tagname> <commit>`- To tag some older commits
- `git tag -f <tagname>`- to replace/move tags forcefully
- `git tag -d <tagname>`- to delete tags
- `git push origin <tagname>`- to push a single tag
- `git push origin --tags`- to push all the tags

---

#### **git reflog** (reflog = reference log)

- `git reflog`- records of when references were updated
  - can be found under `.git/refs` directory in your repository.
  - subcommands - `show` , `expire`, `delete`, `exists`
  
#### **NOTE**: `git log` only includes commits and its parent and so on whereas `git reflog` includes history of things ex: clones, check-outs, deleted commits, etc.

- `git reflog show HEAD`- logs of the references when HEAD was changed
- `git reflog show <branch_name>`- logs of the references when
- `git reflog show HEAD@{10}`- shows all the reference logs from HEADs position 10 moves ago till its position at 
  the beginning of the repository.
  - `HEAD{0}`- refers to the most recent entry in the HEAD reflog

- `git checkout HEAD@{2}`- it takes us back where HEAD was 2 steps before (need not be same branch or can be same 
  branch and even same commit)
- `git checkout HEAD~2`- moves the HEAD back to 2 commits
- ##### Time based reflogs
  - `git reflog master@{one.week.ago]}`
  - `git reflog master@{1.day.ago}`
  - `git reflog master@{yesterday}`

---

#### Git Objects (Notes)

There are 4 types of git objects stored in the objects (/.git/objects) directory in your repository:
1. blob :- binary large object, git uses to store the contents of the files (they don't include the file name)
2. tree :- are git objects used to store the content of the directories. Trees contains pointers that can refer to blobs and to other trees
3. commit :- it combines a tree object along with information about the context that led to the current tree. Commit stores :- a reference to a tree, a reference to parent commit, the author, the commiter and the commit message
4. annotated tag :- it is a pointer to a particular commit

>![img.png](images/img.png)
>  - A `annotated tag` points to a particular `commit`.
>  - A `commit` points to a `tree`.
>  - A `tree` can point to many blobs and other trees

- `git hash-object <file>`- command that provides the hash result using SHA-1 encryption for the content of the file

Example of `git hash-object` command
```
echo "some-text" | git hash-object --stdin
```

- `git cat-file -p <object-hash>`- To retrieve the data from a hash
- `git cat-file -t <object-hash>`- tells the type of the object (blob/ tree/ commit/ annotated tag)
- `git cat-file -p main^{tree}`- command for viewing tree. the syntax main^{tree} specifies the tree object 
  that is pointed to by the tip of our branch 9in this case `main`).


