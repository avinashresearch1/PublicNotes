# Overview
Notes for Pro Git by Scott Chacon, Ben Straub

## Useful shortcuts:

- `git log --all`shows the log for all the commits. Or can do a branch specific log with `git log <branch name>`. Nice ASCII graphics with: `git log --graph <branch name>`. 

## Ch. 1. Basics
- Modified
- Staging Area/Index.
- Committed.

![image](https://user-images.githubusercontent.com/90404321/201479341-f36503cb-8da1-4d68-8606-e5e4c2736980.png)


Working directory, Staging Area, Git local repository/Git directory/compresseed database.

Basic workflow:
1.  Modify files in working tree: Single checkout of one version of the project.
2. Selectively stage. 
3. Commit. Takes files from staging area, stores snapshot permanently in Git directory. 

### Git config:

Contains customization of the Git usage, e.g., my JH git config:

![image](https://user-images.githubusercontent.com/90404321/201473311-d287a839-eac0-4be7-935a-de1b805db8f5.png)


`git config --list` shows the attributes such as `user.name` and `user.email`.

`git config --global` sets all the global data: 

```
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com

git config --global init.defaultBranch main
```

## Git Remotes:

- `git remote`.
- Usually `origin` means the repository we have cloned the working directory from. 
- `git remote -v`: URLs that git has stored.
- Can have multiple remotes: 

![image](https://user-images.githubusercontent.com/90404321/201475598-8ac00b47-d95c-491b-bde5-242be72d72d5.png)


- `git remote add <name> <url>`
- `git fetch <remote> allows getting data from remotes.
- `git push <remote> <branch>.`

### Tagging:
- Tag specific points in the repository as important: 
- `git tag -a v1.4 -m "my version 1.4"`

## Branching:

- When git does branching, the commit object is a pointer to the content that was staged, together with some metadata e.g., authors name and address, message, and pointer to parents. 
- When you **stage** files: Git computes a checksum for each one of them using SHA-1, stores the version of the file in the repository (called a blob). This checksumming and hasing is done for each file.
- When a **commit** is done: Git checksums the entire workspace to give the commit/tree hash. Then creates a commit object, that has the metadata and a pointer to the root project tree.

So git repo now contains:
1. 3 blobs for the files 
2. 1 tree for the directory and the filenames. 
3. 1 commit with the pointer to the root tree and commit metadata.

![image](https://user-images.githubusercontent.com/90404321/201476110-ac721ad7-7e76-4154-883d-e06a35ffd9fe.png)

Now the commits:


![image](https://user-images.githubusercontent.com/90404321/201476271-ebb683e9-d68d-4f7d-ae33-df1fc0389085.png)


- A **branch** in git is a **movable pointer to one of the commits**. Default branch: `main`. Every commit moves the `main` branch forwards automatically. 
- When you create a new branch, you basically get a new pointer. 
- The **HEAD** tells the OS which branch you are currently on: 

![image](https://user-images.githubusercontent.com/90404321/201476357-de9cb86f-b698-4fad-87a9-c311a1c5ddaa.png)

![image](https://user-images.githubusercontent.com/90404321/201476475-8b040f79-853f-4967-acd1-225f25d2c68f.png)

Note that `git log` gives us the commit, and also tells us which pointers are at that commit. So in the example above, we see that the local `HEAD` is pointing to the latest commit on my local main branch.

- `git checkout <new branch>` moves the HEAD to the new branch.
- So when you commit next, the branch to which HEAD points to is the one that moves forward. The `main` branch still points to the commit it was last left at. 

### Merging and Deleting branches

- `git merge new_branch` merges the new branch into `main`. 
- **fast-forward**: This means that we are trying to merge in a  `new branch` commit to an `main branch` commit. The `main branch` commit is a direct ancestor to the `new branch` commit, and can be reached from the new branch commit. 
- `git branch -d merged_branch`

 
### Three way merge
- Creates a new commit for the merge which now has two parents.

![image](https://user-images.githubusercontent.com/90404321/201477562-7d028bca-dee7-4ceb-8a7d-3c0aca550382.png)


![image](https://user-images.githubusercontent.com/90404321/201477611-5d670331-0085-41fc-b19d-160e72687af4.png)


### Merge conflicts:
If the current `main` commit and the incoming commit (based on a different ancestor) change the same code. `git status` shows umerged files.

![image](https://user-images.githubusercontent.com/90404321/201477818-d81a2a29-8fbe-4844-8443-db2161fb04e9.png)

### Renaming a branch:

- `git branch --move master main`.
- Rename a branch on remote too: `git push --set-upstream origin main`

## Synchronizing with remote

- `git fetch origin`.
- **Tracking branch** Is the local branch checkout from a remote branch, the branch it tracks is called **upstream** branch. 
- The `-u` command is a short form form for set upstream. 
- Note once a branch is deleted, Github usually keeps the data for a little while until garbage collection runs. 

## Rebasing vs Merging

- Rebase means take all my changes that I made on one branch and apply them ontop of a new main branch. 

![image](https://user-images.githubusercontent.com/90404321/201478568-49f9e146-50b4-4b24-b0c1-4da775e7cf28.png)


Why use **rebase** over **merge**:
- Gives a cleaner history, everything looks linear. 
- **Do not rebase commits that exist outside your repository and that people may have based work on.**

## Rewriting history:

- `git reset --hard` is one of the only ways in which git deletes data.  

Think of `git reset` as working on the three trees: Working directory, Commited HEAD, and staging area/index.

![image](https://user-images.githubusercontent.com/90404321/201479592-f3f0b4fe-289a-41ee-ae6a-1a0e8e5d0034.png)

`HEAD~` is the parent of head.

![image](https://user-images.githubusercontent.com/90404321/201479651-9534d059-f30c-4467-9c9d-f2289a64f2f6.png)


![image](https://user-images.githubusercontent.com/90404321/201479707-6b41697f-f3ee-4904-8110-c630413bbab3.png)






  
  









































