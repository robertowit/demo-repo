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
        > shows you *main branch marked
    $ git checkout -b demoBranch-1
        > creates new branch
    $ git branch
        > shows new active branch marked with star *demoBranch-1
    



