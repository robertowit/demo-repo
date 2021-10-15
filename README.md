# Headline H1 - This is a demo repo
## Headline H2 - This is a chapter 
This is some plain text - this is a first edit. A commit update information will be added and the commit can be traced (created, updated ...) 

test

This is an intro to install Git & GitHub on Macbook Air 13" M1 (11/2020+), on Win10 Pro 64-bit EN over Parallels version 17.01

0) Git & GitHub installation using 
    - Check if Git available in Powershell / Terminal, 
        $ command: git --version

        The following installation is default (next, path leave as is, ..) with respect to:
            - Add Git Bash profile -> activate check box 
            - Use Visual Studio Code as Git's default editor

    - Git & GitHub tutorial: https://www.youtube.com/watch?v=RGOj5yH7evk (14.10.21)
    - Install and set up Git: https://support.atlassian.com/bitbucket-cloud/docs/install-and-set-up-git/ (14.10.21)
        commands after installation: 
            $ git config --global user.name "<yourGitHubUserName, in git example Emma Paris>"
            $ git config --global user.email "<aourGitHubEMail, eparis@atlassian.com"
            depending on OS
            * for Windows:          $ git config --global core.autocrlf true
            * For Mac and Linux:    $ git config --global core.autocrlf input
    - if Visual Studio Code was already installed: use Administrator rights when starting shortcut VS Code (properties > adv. > admin...)

1) On GitHub
-------------------
1.1) Create GitHub repo (directory demo-repo)
1.2) Create README.md (MarkDown) that should describe what the repo does on GitHub

2) Git in Visual Studio Code (or other Git editor like VIM, Notepad++):
------------------- 
2.1) in Visual Studio Code: open repository containing folder "demo-repo" 
2.2) Created index.html just for test-purpose, made some changes in README.md (for training git status, commit, push, SSHkey, https auth ...)
2.3) SSH key generation: see https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent (14.10.21)
    - Open Git Bash & command:
        $ ssh-keygen -t ed25519 -C "your_email@example.com"
            ... > Enter a file in which to save the key (/c/Users/you/.ssh/id_algorithm):[Press enter]  (f. e. mySSHkey)
                -> this creates mySSHkey and mySSHkey.pub (private and public key), from which later the public one will be added in GitHub.
            ... > Enter passphrase (empty for no passphrase): [Type a passphrase] - I left this open, optional, safer to set
            ... > Enter same passphrase again: [Type passphrase again] - I left this open, optional, safer to set
        If that fails due to permission issues: create a new folder outside Git-folder...
    - Switch in Git Bash to folder with SSH keys (for example C:/users/<yourname>/git-sshkeys)
    - Show the ssh key (public one) content, command:
        $ cat mySSHkey.pub
            -> copy that (via marking or right-click, not CTRL+C) and 
            -> add the content (some letters etc... followed by email)
               in GitHub >> Settings >> SSH ..  https://github.com/settings/keys >> Button "New SSH key" ... add..
    ... refere to top link in case of errors or search for them in the web ... normally some configuration necessary or permission issue from "Program Files" folder or similar issue...

2.4) COMMANDS in Visual Studio Code terminal (powershell) while in repo folder:
    git -- version
        -> dispays version to check if also in terminal available
    git status
        -> check current file status, 2x files should be shown: README.md changes, index.html new
    git add .       // or instead of the dot the folder or file that should be staged
        -> stages the folders/filers, dot(.) = all 
    git status 
        -> could be once more necessary..
    git commit -m "Message of What and Why commited for tracing" -m "(optional) Additional description, do not forget the second -m"
        -> commits the file in the local repo, not yet pushed to remote
    git status 
        -> check if succesfully commited, should be seen in visual studio files/folders tree
        ... but is necessary prior further actions!
    git push
        -> pushs the new commits to the remote repo

.... should result in some messages about Enumerating, 
.... 100 % couting and writing, 
...  ignore Cygwin warning
                                    // Cygwin WARNING:
                        ignore      // Couldn't compute FAST_CWD pointer.  This typically occurs if you're using
                                    // an older Cygwin version on a newer Windows.  Please update to the latest
                                    // available Cygwin version from https://cygwin.com/.  If the problem persists,
                                    // please see https://cygwin.com/problems.html
.... check GitHub, should be up to date! You've done your first push. Later if parallel branches were created, you might need a pull request etc. to be up to date... here we worked with single main/master changes only by one user without branching. 


But what about creating a repo locally and pushing it to GitHub?
1) in VS Code create second folder "demo-repo2" ((move) outside demo-repo, so that it is not part of the other repo)
2) switch to folder demo-repo2:     
    cd ../demo-repo2   
3) create 2nd README.md with some content, see above
4) Tell Git to use the new folder as a repo, add the new file (staging), commit it with message -m "..."
    $ git init              // <<< NEW >>>
    $ git add README.md
    $ git commit -m "2nd git demo repo"
5) On GitHub, create a folder to have a "remote" repo 
6) In VS Code Terminal: set remote repo (see GitHub HTTPS link, SSH did not work in my case... agent / SSH configs necessary)
    $ git remote add origin https://github.com/robertowit/GitHubDemoRepo2.git
    $ git push -u origin master     
        > outputs: ... 100 % ... done

That's it, you just created a local repo and pushed it to the remote target


Git BRANCHING 
----------------------------------------------------------

1) Check on which branch you are (in demo: *main), create a branch with name -b "feature-11" (or "bugfix-1245") and further description etc...
    $ git branch
        > shows you *main branch marked ("main" = former "master")
    $ git checkout -b demoBranch-1
        > creates new branch
    $ git branch
        > shows new active branch marked with star *demoBranch-1
    $ git checkout -b main
        > switches to main again
    $ git branch
        > show you're active on main branch

    // Auto-Fill command / field is possible with TAB if you do not want to write the whole branch name or command    
    $ git checkout -b demoBranch-1

2) Make some changes in the project in new branch, git status + add to stage and commit them

 ... now make some changes... for example in README.me

 ... git status
 ... git add .
 ... git commit -m "Updated readme, training"
 
3) Change to main branch, merge
3.1) Switch to main branch -> **main, show diffs to new branch "demoBranch-1"
    $ git checkout main
    $ git branch
        > check if you're on main branch, *main should be marked
    $ git diff demoBranch-1
        > output shows diffs from main vs. new
    ... now we could call    $ git merge demoBranch-1   ... to merge new branch to main, but common pattern is to push branch to GitHub and Pull-Request afterwards... 
    (PR = Pull-Request is common practice for questions, checks, ... about changes) 
3.2) switch back to NEW branch, git status, add ., commit
    $ git checkout demoBranch-1
    $ git branch
        > make sure you're on new branch
    $ git status
    $ git commit -m "README.md updated, optimized guideline, new branch training"
    $ git push -u origin demoBranch-1
        > ... 100 % ... done ... 
3.3) You can now visually pull-request (PR) or per terminal.... 
A) Visually Pull-Request via GitHub
    
    - Go to GitHub webpage > your demo-repo ... new Button "Compare & pull request" came up  (at 44:51 in https://www.youtube.com/watch?v=RGOj5yH7evk, 14.10.21.),
    ... shows from which to which branch merge will be done...
    ... create a list of made changes ... (history log in Git as commmon practice)
    ... check comments, changes in commits...
    
    - Click Button "Merge pull request"

    - in VS Code you need to pull in main branch the changes 
    VS Code > Terminal > switch to main branch, commands:
        $ git checkout main
        $ git pull

        .... if successfully pulled and changes ok > delete branch in GitHub and locally in Git

        - in GitHub, in repo section "Pull request successfully merged and and closed: button Button DeleteBranch

        - in Git: delete already merged branches (common practice, clean up)
            $ git branch -d demoBranch-1
            $ git branch
                > output should now show only the main branch ... great! :) 

/// BUT NOW - WHAT HAPPEN's WITH MERGE CONFLICTS ?? ///

>> compare & apply manually / stash them

example:
- new main index.html change
- 'your new branch' "testBranch-1" containing changes in index.html
-> conflict
-> stash them by merging changes from main to 'your new branch' (update changes before adding yours via merge into new branch), then comparison of changes manually in editors and rest same way as before  

... some more edit in index.html in branches main / testBranch-1 (via: git branch >> git ceckout main/diffBranch-1 >> git branch)

if in new branch for example testBranch-1 
    $ git merge main
    > ... outputs conflict... merge conflict ... check files... if configured as described above, use VS code to accept new/old changes ... merge then respecitvely... 

    ... after status, add . (or specific folder, file), commit -m "solved merge conflict ...., reason... "...) ...

    ... check GitHub for update, merge via button "Compare pull request", "Confirm..." etc. via git hub

    ... Delete branch (on GitHub)

    ... back in Terminal (locally on Git / Visual Studio Code >> Terminal >> repo folder)
    $ git checkout main
    $ git branch
        > check if in main branch 
    $ git pull newly updated changes are now also locally updated via pull
    ..
    
...



UNDOING GIT
------------------------------------------

Undo an add . = unstage:
    $ git reset (optionally <Folder/Filename   if used in staging via add>)


Undo last commit (same with HEAD~1 or hash to unstage changes):
    $ git reset HEAD~1 (optionally <Folder/Filename)

        // HEAD points to last commit. If we want to undo it, "~1" after HEAD refers to the commit before to which we go back. 

    $ git log
        > shows a list of all commits in reverse chronological order with a hash as a reference. 

If we want to undo until specific commit, use the hash from the commit log:
    $ git reset <hash from a previous git log commit> 
        > unstages until this last commit

  ... or a hard change removal ...
    $ git reset --hard <hash from a previous git log commit>
        > erases latest updates!



FORKING
---------------------------
see tutorial by freeCodeCamp.org: 
https://www.youtube.com/watch?v=RGOj5yH7evk&t=3710s (1:01:50) 

Forking in git creates a complete copy that can be changed for own purpose (~licenses to consider) or to participate in projects and extend them via pull-request and a request for the changes to be added.

To create your own copy:
- In GitHub >> on top right corner Button Fork >> click your user (or group) >> creates complete copy with all branches ... 
- now branching etc. can be used, change in new branches made, merged into main etc...
