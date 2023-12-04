# Lab Report 4 Vim (Week 7)

## Step4: Log into ieng6

### Action:
Used SSH to log into the ieng6 server.
### Screenshot:
![Image](ssh(login).png)
### Key pressed:
```
 $ ssh<space>cs15lfa23en@ieng6.ucsd.edu<enter>
```
Typed the SSH command to connect to the server.

## Step 5: Clone Your Repository

### Action :
Cloned my repository from GitHub using the SSH URL.
### Screenshot:
![Image](gitclone.png)
### Key pressed :
```
 $ git<space>clone<space>git@github.com:NaruKoba/lab7.git<enter>
```
Entered the git clone command followed by the SSH URL of my repository.

## Step 6: Run the Tests (Demonstrating Failure)

### Action:
Executed the tests in my project to show that they failed initially.
### Key pressed:
```
 $ cd<space>lab7/<enter>
```
change current directory to lab7 directory

### Screenshot:
![Image](bash(fail).png)

### Key pressed:
```
 $ bash<space>tes<tab>.sh<enter>
```
`<tab>`: Names can be autofilled by pressing the Tab key, if the they exist.
Typed bash test.sh to compile all of java files and run ListExamplesTests in lab7 directory.

## Step 7: Edit the Code File (ListExamples.java)

### Action:
Opened ListExamples.java and corrected the error in the merge method (change index1 to index2 in the final loop).
### Screenshot:
![Image](vim.png)
### Key pressed:
```
$ vim<space>List<tab>.java<enter>

```
Inside of ListExamples.java:

Typed `:44<enter>` to get to the error line and pressed `< l >` 6 times <l><l><l><l><l><l> for the cursor to be next to 1. Pressed `< i >` to change normal mode to insert mode. Pressed `< backspace >` to delete 1 and typed `< 2 >`. Pressed `<esc>` to return to normal mode. Pressed `:wq<enter>` to save changes and quit from vim editor. 



## Step 8: Run the Tests (Demonstrating Success)

### Action:
Re-run the tests to demonstrate that my code changes have fixed the issue.
### Screenshot:
![Image](bash(success).png)
### Key pressed:
```
$  bash<space>test.sh<enter>

```
Similar to step 6, typed bash test.sh to recompile and run the tests.


## Step 9: Commit and Push Changes

### Action:
Committed the corrected file to my local Git repository and then pushed the changes to my GitHub account.
### Screenshot:
![Image](gitaddcommitpush.png)
### Key pressed:
```
$   git<space>add<space>List<tab>.java<enter>
$   git<space>commit<space>-m<space>"fixed<space>indecies"<enter>
$   git<space>push<enter>
```
Used `git add` to change in my working directory to the staging area. The staging area is like a prep zone for changes before they are committed. 
Used `git commit` to take the staged changes and create a new commit with them in the local repository.
Used `git push` to upload the local repository content to a remote repository. This is how I transfer commits from my local repository to a remote repo (like GitHub).






