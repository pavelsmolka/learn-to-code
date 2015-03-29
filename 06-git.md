#Lesson 6

Version control - Git

##Theory
 - We want to back up our data.
 - We need to be able to view history of all files, when the changes happened and who made them.
 - We need to allow more people to work on one codebase.
 - VCS (version control systems) solve these problems.
 - Centralized systems vs distributed.
 - Git is distributed, the far most popular nowadays.
 - When more people create something simultaneously, we cannot number the commits - we use hashes instead.
 - Hash is a "fingerprint" of any string (you can hash whole book). 
   - For the same input, the output is always identical!
   - It is very rare (almost impossible) to create a hash collision.

##Hands on
 - Create a git repository for testing Hawk API on GitLab.
 - Get a clone of the repository on your Mac. Be aware you have a full clone, not just a working copy.
 - Create a new file, or modify an existing one.
 - Add the file to the staging state using `git add`.
 - Commit the change.
 - Check the commit hash using `git log` or `gitk`.
 - Push your change to GitLab (`git push`).
 - Do some change in the project, commit. Check the new commit hash.
 - Push the new commit to GitLab.
 - Tag your latest commit, push the tag (`git tag <tagname>`). Check existing tags (`git tag`).
 - Check that the change has appeared on GitLab.
 - Create a program which calculates a `sha1` hash of your name. What are the chances someone else's name would result in the same name?

##Homework
 - Create a new GitLab repository for your homework in your personal namespace (dan.burden). From now on, you will commit & push your homework to GitLab, and I will pull it from there. Please, make sure you grant me permissions to (at least) read from the repo (settings -> members).
 - Start building the Testing Hawk API project using the knowledge you have:
   - First of all, create a "design" of what you will try to achieve (pen & paper, or whiteboard). It does not have to be able to do much in the beginning.
   - Choose the right level of abstraction, and decompose your system into individual functions.
   - Start with implementation.
   - Remember we have live and staging API (we need to test both), and on each API there are various combinations of parameters (different widgets, territories, execution types, different sites and article IDs/URLs ...).

##References + Reading
http://git-scm.com/book/en/v2
