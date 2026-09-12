Git Practical — Step 1 to 41
Part 1: Create a directory and initialize Git
1. Create a folder
mkdir Set1

Creates a directory named Set1.

Go inside it:

cd Set1

To see the files/folders:

ls
2. Initialize Git
git init

This converts the Set1 folder into a Git repository.

You will see something like:

Initialized empty Git repository...
Part 2: Configure Git
3. Set your username
git config --global user.name "Your Name"

Example:

git config --global user.name "Smit"
4. Set your email
git config --global user.email "your@email.com"

Example:

git config --global user.email "smit@gmail.com"

Tip: For GitHub, it is best to use the email associated with your GitHub account.

5. Proxy — only if your network requires it

Your notebook has:

git config --global http.proxy 192.168.0.253

But do not run this unless your college/company network actually requires a proxy.

If you don't need a proxy, skip this step.

If you previously configured a wrong proxy, remove it with:

git config --global --unset http.proxy
6. Check Git configuration

The incomplete command in your notebook should be:

git config --list

This displays your Git configuration.

You can also specifically check:

git config --global user.name
git config --global user.email
Part 3: Create your first file
7. Create README.md
echo "This is read me file" > README.md

This creates a file called:

README.md

with the text:

This is read me file

Check it:

cat README.md
Part 4: Check and commit the file
8. Check Git status
git status

You should see README.md as an untracked file.

Something similar to:

Untracked files:
    README.md
9. Add README.md to staging
git add README.md

This puts the file into the staging area.

10. Check status again
git status

Now README.md should appear as a new file to be committed.

11. Create your first commit
git commit -m "This is my first commit in main branch"

This permanently records the staged file in Git history.

12. Check status
git status

You should normally see:

nothing to commit, working tree clean
Part 5: Main branch
13. Rename current branch to main
git branch -M main

This makes your current branch:

main
14. Check branches
git branch

You should see:

* main

The * means you are currently on that branch.

Part 6: Connect Git to GitHub

First, create a new repository on GitHub.

For example, suppose your GitHub repository is:

https://github.com/yourusername/Set1.git
15. Add GitHub as remote
git remote add origin YOUR_GITHUB_LINK

Example:

git remote add origin https://github.com/smit/Set1.git

origin is simply the standard name given to your remote GitHub repository.

Check it:

git remote -v
16. Push main branch to GitHub
git push -u origin main

The -u connects your local main branch with the remote origin/main.

After this, your README should appear on GitHub.

Part 7: Modify the README
17. Add another line to README.md
echo "HELLO" >> README.md

Important:

> creates/overwrites a file.
>> adds to the end of an existing file.

Your README now contains:

This is read me file
HELLO
18. Add the modified file
git add README.md
19. Commit the modification
git commit -m "This is my second commit"
20. Push the second commit
git push -u origin main

You could also simply use:

git push

because the upstream was established in Step 16.

Part 8: Create a new feature branch

Now we create a branch called:

feature/login
21. Create and switch to the branch

Your notebook says:

git checkout -b feature/login

This is correct.

It does two things at once:

Creates feature/login
Switches to feature/login

You should see:

Switched to a new branch 'feature/login'
22. Check the branch
git branch

You should see:

* feature/login
  main

The * tells you that you're currently working on feature/login.

Part 9: Create login file
23. Create login.md
echo "feature login" > login.md

This creates:

login.md
24. Add login.md
git add login.md
25. Commit the feature
git commit -m "This is feature login"
Part 10: Push feature branch
26. Push feature/login to GitHub
git push -u origin feature/login

Now GitHub will contain two branches:

main
feature/login
Part 11: Go back to main
27. Switch to main
git checkout main

Now you are back on:

main

You can verify:

git branch
28. Check branches
git branch

Expected:

  feature/login
* main
Part 12: Merge feature/login into main
29. Merge the feature branch
git merge --no-ff feature/login
What does --no-ff mean?

It means Git will create a separate merge commit, even if Git could merge the branches using a fast-forward.

This makes the branch history easier to see.

You may get an editor asking for a merge commit message.

You can accept the default message.

30. Push the merged main branch
git push

Now the feature/login changes are also present in main.

Part 13: Create a Semantic Version Tag

A tag is used to mark a particular version of your project.

For example:

v1.0.1

This follows Semantic Versioning:

vMAJOR.MINOR.PATCH

For example:

v1.0.0
v1.0.1
v1.1.0
v2.0.0
31. Create an annotated tag

Your notebook says:

git tag -a v1.0.1 -m "This is Version 1"

A cleaner version would be:

git tag -a v1.0.1 -m "This is Version 1.0.1"

This creates an annotated tag named:

v1.0.1
32. Push the tag to GitHub
git push origin v1.0.1

Now the tag will be available on GitHub.

You can see your tags with:

git tag
Part 14: Make another change on main

You are currently on main.

33. Modify login.md
echo "This is another change" >> login.md

Now another line is added to login.md.

34. Check status
git status

Git should show that:

login.md

has been modified.

35. Stage the modified file
git add login.md
36. Commit the change
git commit -m "My another commit"
37. Push the new main commit
git push -u origin main

Since upstream is already configured, this could also simply be:

git push
Part 15: Update feature/login with main

Now we go back to the feature branch.

38. Switch to feature/login
git checkout feature/login
39. Check branches
git branch

You should see:

  main
* feature/login
40. Merge main into feature/login
git merge --no-ff main

This brings the latest changes from main into:

feature/login

So now your feature branch is updated with the latest main branch.

41. Push feature/login
git push

Done. ✅
