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
git add .
```

We're on branch `master`, but we may not want to push directly there, to protect the integrity of the production code. Let's make a new one.



```bash

```