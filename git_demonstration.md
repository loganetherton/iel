# Git Demonstration

## Initialize Repository

```bash
git init
```

This is going to initialize an empty repository where we can commit our code.

```bash
git branch

/p/s/iel ❯❯❯ git branch                                                                                                                                                                                                           ✘ 1 
/p/s/iel ❯❯❯ 

```

We have some files, so let's stage them:

```bash
git status
/p/s/iel ❯❯❯ git status                                                                                                                                                                                                         ✘ 128 
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	git_demonstration.md
	node_modules/
	package.json
	question_2.js
	question_2.txt
	question_3.js
	question_3.txt
	yarn.lock

/p/s/iel ❯❯❯ git add .
/p/s/iel ❯❯❯ git status
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   git_demonstration.md
	new file:   node_modules/.yarn-integrity
	new file:   node_modules/date-fns/CHANGELOG.md
....

```

Whoops! We have `node_modules`, which we don't want to commit to our repository. Let's undo that:

```bash
/p/s/iel ❯❯❯ git reset .
/p/s/iel ❯❯❯ git status
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	git_demonstration.md
	node_modules/
	package.json
	question_2.js
	question_2.txt
	question_3.js
	question_3.txt
	yarn.lock

```

Much better! Everything is unstaged. Now, let's create a `.gitignore`	file to prevent adding `node_modules` again:

```bash
/p/s/iel ❯❯❯ touch .gitignore && echo node_modules \\nanother_dir \\nsecret.key >> .gitignore
/p/s/iel ❯❯❯ cat .gitignore
node_modules 
another_dir 
secret.key
```

Now let's try staging the files again:

```bash
/p/s/iel ❯❯❯ git add .
/p/s/iel ❯❯❯ git status
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   .gitignore
	new file:   git_demonstration.md
	new file:   package.json
	new file:   question_2.js
	new file:   question_2.txt
	new file:   question_3.js
	new file:   question_3.txt
	new file:   yarn.lock

```

OK! We're ready to make our initial commit:

```bash
/p/s/iel ❯❯❯ git commit -m 'Initial commit'                                                                                                                                                                                     ✘ 128 
[master (root-commit) 3c8e0d4] Initial commit
 8 files changed, 467 insertions(+)
 create mode 100644 .gitignore
 create mode 100644 git_demonstration.md
 create mode 100644 package.json
 create mode 100644 question_2.js
 create mode 100644 question_2.txt
 create mode 100644 question_3.js
 create mode 100644 question_3.txt
 create mode 100644 yarn.lock
****
```

Let's take a look back and see if we're ok with everything we've done thus far:

```bash
/p/s/iel ❯❯❯ git log
commit 3c8e0d4ec5f7e5b58aabfd47fce4806e55581878
Author: logan <loganetherton@gmail.com>
Date:   Thu Dec 12 12:26:54 2019 -0500
```

We're on branch `master`, but we have a whole team of folks who need to be commit to this repository. We should make another branch for this untested code:

```bash
/p/s/iel ❯❯❯ git branch secret master                                                                                                                                                                                           ✘ 128 
/p/s/iel ❯❯❯ git branch
* master
  secret
```

Now we've got our own secret branch! Let's get on it:

```bash
/p/s/iel ❯❯❯ git checkout secret                                                                                                                                                                                                ✘ 128 
M	git_demonstration.md
Switched to branch 'secret'
```
