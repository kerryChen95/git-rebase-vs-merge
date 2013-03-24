# Git: rebase V.S. merge

example is better than explain, this project tell you the difference between rebase and merge in Git.


first of all, commits tree as below:

```JavaScript
A -- B -- D  <-- master
      \
       C -- E  <-- topic
```
---

I try a **rebase operation**: on branch topic, run `git rebase master`, commits tree as below:

```JavaScript
A -- B -- D -- C -- E
          ^         ^
          |         |
        master     topic
```

in this project, before get such commits tree, I have to **resolve a rebase conflict** in below steps:

1. edit test.md: keep the content from branch master, remove the conflict content from branch topic
2. run `git add test.md` to tell git the conflict in test.md have been resolved
3. run `git rebase --continue` to continue rebase

---

after that, I notice master HEAD still refer to commit D, so run `git merge topic` on branch master and then commits tree as below:

```JavaScript
A -- B -- D -- C -- E  <-- master
                    ^
                    |
                  topic
```
---

next, I try a **merge operation**. Bute before it, I add two commit on branch topic and one on branch master, they are like below:

```JavaScript
A -- B -- D -- C -- E -- H  <-- master
                     \
                      F -- G  <-- topic
```
---

then switch to branch master, it's time to run `git merge topic`, after that, commits tree as below:

```JavaScript
A -- B -- D -- C -- E -- H -- "merge 'topic' commit"  <-- master
                     \       /
                      F -- G  <-- topic
```

notice that topic HEAD still refer to commit G, but master HEAD now refer to a new commit "merge 'topic' commit".

---

finally I add a new commit on topic just to see where it go:

```JavaScript
A -- B -- D -- C -- E -- H -- "merge 'topic' commit"  <-- master
                     \       /
                      F -- G  -- I  <-- topic
```

Yell! Difference between rebase and merge now is clear : P
