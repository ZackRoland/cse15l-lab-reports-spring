## **LAB 4 - VIM**
---
STEP 4:
![ssh](https://i.postimg.cc/nL4JW7yF/image-2024-05-22-225728646.png)
```
ssh<space>zroland@ieng6.ucsd.edu<enter>
```
> Ran ssh with my email to log into ieng6

STEP 5:
![ssh git clone](https://i.postimg.cc/RZb6Frh6/Screenshot-2024-05-22-at-10-05-21-PM.png)
```
git<space>clone<space>git@github.com:ZackRoland/lab7.git<enter>
```
> To clone my fork from my repository I copied the SSH option and ran
> git clone with it.

STEP 6:
![Failed Tests](https://i.postimg.cc/cC9ZmSVf/image-2024-05-22-225610414.png)
```
cd<space>lab7/<enter>
bash<space>test.sh
```
> To run the tests, first had to cd into the cloned directory. Then i
> ran the test files in test.sh with bash.

STEP 7:

![vim](https://i.postimg.cc/T3h1Bk0R/Screenshot-2024-05-22-at-10-03-00-PM.png)
```
vim<space>ListExamples.java<enter> 44G 1e r2 :wq <enter>
```
> First off I opened the ListExamples file with vim to edit it.
> To fixed the code that was causing the errors, I had to change the 1
> in index1 to a 2 as specified. The line of this error as identfied in previous
> instances of running this is in 44 so I type 44G to move the cursor directly
> in the first line. Since the error is at the end of the first word I typed 1e
> which moved my cursor directly above the 1. Since that was the only thing that
> needed changing, what I did was type r2 to replace whatever was on my cursor with
> the 2. Finally to save the changes I typed in :wq then enter.

STEP 8:
![Test Success](https://i.postimg.cc/fbp9H4hn/Screenshot-2024-05-22-at-10-03-57-PM.png)
```
bash<space>test.sh
```
> To rerun the tests I had to run bash on the test file again.

STEP 9:
![git commit](https://i.postimg.cc/ydh8021T/Screenshot-2024-05-22-at-10-07-36-PM.png)
![git push](https://i.postimg.cc/HW2LnGPY/Screenshot-2024-05-22-at-10-09-17-PM.png)
```
git<space>add<space>.<enter>
git<space>commit<enter>
G<space>Fixed<space>Errors!<esc>:wq<enter>
git<space>push<enter>
```
> To commit and push the changes to my github had to git add, git commit and
> git push in that order. With git add i have a period after to add all changes.
> Then with git commit im able to go in and add a commit message in which I
> made my message "Fixed Errors!". Then to save that message I escaped and typed
> :wq. Finally running git push pushed the commit over to github.
