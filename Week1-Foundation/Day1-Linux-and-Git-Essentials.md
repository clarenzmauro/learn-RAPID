linux deep dive
basic terminal commands
- cd - change directory
- ls - list
- sudo - substitute user do
- pwd - print working directory
- mkdir / rmdir - make/remove directory
    - example usage:
        - mkdir my_new_project
        - cd my_new_project
        - pwd
        - cd ..
        - rmdir my_new_project
            - for non-empty dir, use rm -rf (remove, recursively, force)
- touch / rm - create/remove files
    - example usage:
        - mkdir test_folder
        - cd test_folder
        - touch my_file.txt
        - ls
        - rm my_file.txt
        - ls
        - cd ..
        - rmdir test_folder
- cp / mv - copy/move files and dir
    - example usage:
        - touch original.txt
        - cp original.txr copy.txt
        - ls
        - mv copy.txt renamed.txt
        - ls
- cat / nano - view/edit file content
    - example usage:
        - touch notes.txt
        - nano notes.txt # cmd + s to save, cmd + x to exit
        - cat notes.txt
- apt - advanced package tool
    - example usage:
        - sudo apt update
        - sudo apt upgrade -y # -y automatically confirms prompts

git and github
git is your local version control system
github is a cloud-based hosting service for git repo where you can remotely, collaborate, and often where CI/CD runs

main commands/concept:
- git init - initializes a new git repo in your current dir
- git clone [url] - downloads an existing git repo from a url
- git add [file] - stages changes for the next commit
- git commit -m "message" - creates a snapshot of your staged changes with a message
- git push - uploads your local commits to the remote repo
- git remode add origin [url] - connects your local repo to a remote one. origin is a common nickname for the primary remote
- .gitignore - a file where you list files/folders that git should ignore

day 1 mini-project
1. create a project folder then initalize git
2. login and create a new repo on github
3. connect your local repo to github
4. create a readme.md 
5. add, commit, and push your changes