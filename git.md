- GIT(global information tracker)
![alt text](image-37.png)
![alt text](image-38.png)
```
1) jis folder ko tmko git version control mein daalna hai wohan jaake git init daalo
2) usme .git ki file aa jayegi and how to check , ye hmesha chupa rhega , check by typing ls -a means show all folders(hidden folders too)
3) to check all the commands associated with it , egs - use (man ls) it will show all commands associated with ls
4) to check whether your files are untracked, tracked,staged or not - use git status
5) to move from untracked to staged - use git add .
6) aur tmko wapas staged se untracked mein bhejna hai toh use - git rm --cached {file_name}
7) agar tmko staged se tracked jana hai toh - git commit
8) let say u remove the file , so it will be removed from file system but can be taken back by writing ( git restore {file_name})
9) to config ur name use git config --global user.name rishiraj 
10) to config ur email use git config --global user.name {email id}
11) to see all the history type git log
```
## tree
![alt text](image-39.png)
![alt text](image-40.png)
![alt text](image-41.png)
![alt text](image-42.png)
```
to check branches - git branch
to create a new branch- git checkout -b dev
- if you checkout and add new file in vcs then it starts from where u leave main branch
- ye automatically master branch mein ni aa jata hai
- git checkout branch name se branch switch hota hai aur -b add krne se naya branch aur switch hote ho
- git log --online se one line comment aayega
- head matlab latest commit jaise image shown hai latest commit add readme hai
- agar dev branches ke changes master branch mein daalna hai- git merge dev


```
- git workflow
```
Start fresh: Always make sure your local computer is up to date before starting new work.
git checkout main
git pull origin main
Create your sandbox: Create your new branch for your specific task.
git checkout -b feature/my-cool-new-button

Write code and save: Do your work, add, and commit.
git add .
git commit -m "Add cool new button"
Push your specific branch: Send only your branch up to GitHub.
git push origin feature/my-cool-new-button

The Staging Phase (Testing):
Go to GitHub and open a Pull Request asking to merge feature/my-cool-new-button into staging.
Your team reviews the code. Once approved, you click the "Merge" button on GitHub.
The QA (Quality Assurance) team tests the app on the staging server to make sure your button works and doesn't break anything else.

The Main Phase (Production):
Once everything in staging is tested and confirmed working, a new Pull Request is opened to merge staging into main.
When that PR is merged, your code goes live to the real users!

```
![alt text](image-43.png)
![alt text](image-44.png)
![alt text](image-45.png)
![alt text](image-46.png)
## how to transfer local git repo to remote git repo

```
1) first check kro ki tmhara local git remote git se connected hai ki ni- git remote -v
2) tm dekhoge ki origin likha hoga woh https se connect hua hoga jab tmhara connect hoga woh url ke liye hota hai origin
3) then u can push git push origin master means master branch remote mein bnega aur wohan push ho jayega
4) lekin tmse username aur password maangega toh personal access token se baar baar ni puchega
5) git remote set-url origin https://{Pat}@github.com/irajspace/repo-name.git
6) lets say there are some files which are in remote and in your local - then git pull origin master- remote ke master branch se current branch mein la dega 

```

## how can u take remote repo to ur local
![alt text](image-47.png)

```

1) clone - isme do tarah hota hai pat aur ssh 
2) if ssh -how to generate ssh-pair key (means private public key)- ssh-keygen
3) to see diff use git diff
4) kisi bhi public repo ko pull krne mein ssh ya pat ni lgti only for pushing changes lgti hai
5)git clone  = download an existing Git repository + initialize it
6) jaise tmne kisi repo ko clone kr liya usme check kro woh uska origin ... git remote -v se... ye output aayega ..origin  https://github.com/someone/project.git
7) then u can remove git remote remove origin, then u can add urs origin  https://github.com/someone/project.git

```
## forking vs cloning
![alt text](image-48.png)

## git branching strategies
![alt text](image-49.png)
```

```
