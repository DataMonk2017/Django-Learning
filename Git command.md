$ ssh-keygen -t rsa -C "github emaill account"
Generating public/private rsa key pair.
Enter file in which to save the key (/z//.ssh/id_rsa):
Created directory '/z//.ssh'.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /z//.ssh/id_rsa.
Your public key has been saved in /z//.ssh/id_rsa.pub.
The key fingerprint is:

The key's randomart image is:

$ cat ~/.ssh/id_rsa.pub

$ ssh -T git@github.com
The authenticity of host 'github.com (192.30.253.113)' can't be established.
RSA key fingerprint is SHA256:
Are you sure you want to continue connecting (yes/no)? T
Please type 'yes' or 'no': yes
Warning: Permanently added 'github.com,192.30.253.113' (RSA) to the list of known hosts.
Enter passphrase for key '/z/.ssh/id_rsa':
Hi DataMonk2017! You've successfully authenticated, but GitHub does not provide shell access.

$ git clone https://github.com/DataMonk2017/Hello-Git.git
Cloning into 'Hello-Git'...
remote: Counting objects: 3, done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.

$ cd Hello-Git

$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Untracked files:
  (use "git add <file>..." to include in what will be committed)

        helloworld.php.txt

nothing added to commit but untracked files present (use "git add" to track)

$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Untracked files:
  (use "git add <file>..." to include in what will be committed)

        helloworld.php

nothing added to commit but untracked files present (use "git add" to track)

$ git add helloworld.php

$ git commit -m "Add hello world script by php"
[master cd0f6fd] Add hello world script by php
 Committer: Jeremy Zheng <Jeremy@c2c.local>
Your name and email address were configured automatically based
on your username and hostname. Please check that they are accurate.
You can suppress this message by setting them explicitly. Run the
following command and follow the instructions in your editor to edit
your configuration file:

    git config --global --edit

After doing this, you may fix the identity used for this commit with:

    git commit --amend --reset-author

 1 file changed, 3 insertions(+)
 create mode 100644 helloworld.php

$ git log
commit cd0f6fdf6cec19315dfefa63c21fb2ad8bb9edeb
Author: Jeremy Zheng <Jeremy@c2c.local>
Date:   Fri Apr 14 16:25:48 2017 -0400

    Add hello world script by php

commit a75e5619c68dd792f8793ffc69ad2bda0bc70fae
Author: Jeremy Zheng <DataMonk2017@users.noreply.github.com>
Date:   Fri Apr 14 16:18:00 2017 -0400

    Initial commit

#please use ssh method
$ git remote set-url origin git@github.com:DataMonk2017/Hello-Git.git

$ git push
Enter passphrase for key '/z/.ssh/id_rsa':
Counting objects: 3, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 324 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To github.com:DataMonk2017/Hello-Git.git
   a75e561..cd0f6fd  master -> master

$ mkdir git-tutorial

$ cd git-tutorial

$ git init
Initialized empty Git repository in Z:/git-tutorial/Hello-Git/git-tutorial/.git/

$ git status
On branch master

Initial commit

nothing to commit (create/copy files and use "git add" to track)

$ touch README.md

$ git status
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        README.md

nothing added to commit but untracked files present (use "git add" to track)

$ git add
Nothing specified, nothing added.
Maybe you wanted to say 'git add .'?

$ git add README.md

$ git commit -m "First commit"
[master (root-commit) 4b9bb66] First commit
 Committer: Jeremy Zheng <Jeremy@c2c.local>
Your name and email address were configured automatically based
on your username and hostname. Please check that they are accurate.
You can suppress this message by setting them explicitly. Run the
following command and follow the instructions in your editor to edit
your configuration file:

    git config --global --edit

After doing this, you may fix the identity used for this commit with:

    git commit --amend --reset-author

 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 README.md

$ git commit
On branch master
nothing to commit, working tree clean

$ git status
On branch master
nothing to commit, working tree clean

$ git log
commit 4b9bb668ebcc97fb1f6be82cd8ea1800f9f907c4
Author: Jeremy Zheng <Jeremy@c2c.local>
Date:   Fri Apr 14 16:37:07 2017 -0400

    First commit

$ git log --pretty=short
commit 4b9bb668ebcc97fb1f6be82cd8ea1800f9f907c4
Author: Jeremy Zheng <Jeremy@c2c.local>

    First commit

$ git log README.md
commit 4b9bb668ebcc97fb1f6be82cd8ea1800f9f907c4
Author: Jeremy Zheng <Jeremy@c2c.local>
Date:   Fri Apr 14 16:37:07 2017 -0400

    First commit


$ git log -p
commit 4b9bb668ebcc97fb1f6be82cd8ea1800f9f907c4
Author: Jeremy Zheng <Jeremy@c2c.local>
Date:   Fri Apr 14 16:37:07 2017 -0400

    First commit

diff --git a/README.md b/README.md
new file mode 100644
index 0000000..e69de29

$ git log -p README.md
commit 4b9bb668ebcc97fb1f6be82cd8ea1800f9f907c4
Author: Jeremy Zheng <Jeremy@c2c.local>
Date:   Fri Apr 14 16:37:07 2017 -0400

    First commit

diff --git a/README.md b/README.md
new file mode 100644
index 0000000..e69de29

$ git diff

$ git diff
diff --git a/README.md b/README.md
index e69de29..67a6285 100644
--- a/README.md
+++ b/README.md
@@ -0,0 +1 @@
+# Git??
\ No newline at end of file

$ git diff HEAD
diff --git a/README.md b/README.md
index e69de29..67a6285 100644
--- a/README.md
+++ b/README.md
@@ -0,0 +1 @@
+# Git??
\ No newline at end of file


$ git commit -m "Add index"
On branch master
Changes not staged for commit:
        modified:   README.md

no changes added to commit


$ git log
commit 4b9bb668ebcc97fb1f6be82cd8ea1800f9f907c4
Author: Jeremy Zheng <Jeremy@c2c.local>
Date:   Fri Apr 14 16:37:07 2017 -0400

    First commit


$ git add README.md

$ git log
commit 4b9bb668ebcc97fb1f6be82cd8ea1800f9f907c4
Author: Jeremy Zheng <Jeremy@c2c.local>
Date:   Fri Apr 14 16:37:07 2017 -0400

    First commit

$ git commit -m "Add index"
[master 12230ee] Add index
 Committer: Jeremy Zheng <Jeremy@c2c.local>
Your name and email address were configured automatically based
on your username and hostname. Please check that they are accurate.
You can suppress this message by setting them explicitly. Run the
following command and follow the instructions in your editor to edit
your configuration file:

    git config --global --edit

After doing this, you may fix the identity used for this commit with:

    git commit --amend --reset-author

 1 file changed, 1 insertion(+)


$ git log
commit 12230ee708307f2ade95c5b554725e7df882e888
Author: Jeremy Zheng <Jeremy@c2c.local>
Date:   Fri Apr 14 16:45:25 2017 -0400

    Add index

commit 4b9bb668ebcc97fb1f6be82cd8ea1800f9f907c4
Author: Jeremy Zheng <Jeremy@c2c.local>
Date:   Fri Apr 14 16:37:07 2017 -0400

    First commit

$ git branch
* master

$ git checkout -b
error: switch `b' requires a value
usage: git checkout [<options>] <branch>
   or: git checkout [<options>] [<branch>] -- <file>...

    -q, --quiet           suppress progress reporting
    -b <branch>           create and checkout a new branch
    -B <branch>           create/reset and checkout a branch
    -l                    create reflog for new branch
    --detach              detach HEAD at named commit
    -t, --track           set upstream info for new branch
    --orphan <new-branch>
                          new unparented branch
    -2, --ours            checkout our version for unmerged files
    -3, --theirs          checkout their version for unmerged files
    -f, --force           force checkout (throw away local modifications)
    -m, --merge           perform a 3-way merge with the new branch
    --overwrite-ignore    update ignored files (default)
    --conflict <style>    conflict style (merge or diff3)
    -p, --patch           select hunks interactively
    --ignore-skip-worktree-bits
                          do not limit pathspecs to sparse entries only
    --ignore-other-worktrees
                          do not check if another worktree is holding the given ref
    --progress            force progress reporting


$ git checkout -b feature-A
Switched to a new branch 'feature-A'

$ git branch feature-A
fatal: A branch named 'feature-A' already exists.

$ git branch
* feature-A
  master

$ git add README.md


$ git commit -m "Add feature-A"
[feature-A 3dc3352] Add feature-A
 Committer: Jeremy Zheng <Jeremy@c2c.local>
Your name and email address were configured automatically based
on your username and hostname. Please check that they are accurate.
You can suppress this message by setting them explicitly. Run the
following command and follow the instructions in your editor to edit
your configuration file:

    git config --global --edit

After doing this, you may fix the identity used for this commit with:

    git commit --amend --reset-author

 1 file changed, 3 insertions(+), 1 deletion(-)

$ git branch
* feature-A
  master

$ git checkout master
Switched to branch 'master'

$ cat README.md
# Git??


$ git checkout master
Already on 'master'


$ git checkout feature-A
Switched to branch 'feature-A'

$ cat README.md
# Git??

- feature-A

$ git checkout master
Switched to branch 'master'

$ git checkout -
Switched to branch 'feature-A'

$ git checkout master
Switched to branch 'master'

$ git merge --no-ff feature-A
Vim: Error reading input, exiting...
Vim: Finished.

#shft+z+shfit+z to quite vim editor
$ git merge --no-ff feature-A
Merge made by the 'recursive' strategy.
 README.md | 4 +++-
 1 file changed, 3 insertions(+), 1 deletion(-)

$ git log --graph
*   commit 2dfbd0c1812c9674bd89f8de68846329eafddade
|\  Merge: 12230ee 3dc3352
| | Author: Jeremy Zheng <Jeremy@c2c.local>
| | Date:   Fri Apr 14 17:01:54 2017 -0400
| |
| |     Merge branch 'feature-A'
| |
| * commit 3dc3352584291b363e34b12a207c1352937d5bac
|/  Author: Jeremy Zheng <Jeremy@c2c.local>
|   Date:   Fri Apr 14 16:51:18 2017 -0400
|
|       Add feature-A
|
* commit 12230ee708307f2ade95c5b554725e7df882e888
| Author: Jeremy Zheng <Jeremy@c2c.local>
| Date:   Fri Apr 14 16:45:25 2017 -0400
|
|     Add index
|
* commit 4b9bb668ebcc97fb1f6be82cd8ea1800f9f907c4
  Author: Jeremy Zheng <Jeremy@c2c.local>
  Date:   Fri Apr 14 16:37:07 2017 -0400

      First commit


