# DJANGO-GITHUB

## Part 0: Introduction and Initial Setup
This is the first technical section in the Modern Django guide. Here we will walk through the setup, installation and creation of a Django project. We will also create a GitHub repository for this project during the process.

I truly want this guide, especially this initial portion, to remove barrier to entry to Django development, so excuse the detailed explanation on tools many consider basic. 

A problem many new developers face is they are unaware of standards and best practices for setting up a project. By clearing that up, it will allow them to create and contribute meaning content to Django projects.


## Planning our trip into Django! (source)

### Technology
pip: “The PyPA recommended tool for installing Python packages” (source). Use pip to manage what Python packages the system or a virtualenv has available.
Virtualenv: “A tool to create isolated Python environments” (source). We will use virtualenv to create a environment where the tools used will not interfere with the system’s local Python instance.
Django: “Django is a high-level Python Web framework that encourages rapid development and clean, pragmatic design.” (source). We will install Django using pip.
Git: “A version control system (VCS) for tracking changes in computer files and coordinating work on those files among multiple people” (source).
GitHub: “A web-based Git or version control repository and Internet hosting service. It offers all of the distributed version control and source code management (SCM) functionality of Git as well as adding its own features. It provides access control and several collaboration features such as bug tracking, feature requests, task management, and wikis for every project.[3]” (source).
Other technologies will include your terminal emulator and text editor of choice. I will be using iTerm and Sublime Text 3, but please feel free to use whatever you are comfortable with.

### Walkthrough
Installation
Disclaimer: Here we will begin installing the base tools needed to run a Django project. Many users will have these tools installed already, so if you do; carry on. Nevertheless, it is important not to exclude new users who have not seen or used these tools. Even the understanding that a system may already have a Python instance installed may be foreign to some users!

Also, note that the below commands may be different for users of other POSIX based environments. Typically, you will see python instead of python3 and pip instead of pip3. This is simply due to the fact that MacOS Sierra has an instance of Python 2.7 installed by default and installing the second instance will provide new terminal commands.

1. Install Python
We will assume a fresh install of UBUNTU (or other operating system), thus installing Python 3 is not required.

# Command to check python version.
```
python3 --version
```
# Expected Output
```
Python 3.6.0
```
2. Install Pip
Check that it is also installed by entering the command below.

# Command
```
pip3 --version
```
# Expected Output
```
pip 9.0.1 from /Library/Fram ... (python 3.6)
```

3. Install Virtualenv

# Command
```
pip3 install virtualenv
```

# Expected Output
```
Collecting virtualenv
  Downloading virtualenv-15.1.0-py2.py3-none-any.whl (1.8MB)
    100% |████████████████████████████████| 1.8MB 696kB/s
Installing collected packages: virtualenv
Successfully installed virtualenv-15.1.0
```

Some users may have to make use of sudo (the ability to use permissions of another user, in this case the superuser) when installing virtualenv, show below:

# Command
```
sudo pip3 install vitualenv
```
# Expected Output
```
Password:
```

4. Install git
Most systems will already have git installed. Regardless, it is important to check for this, and if the system git is not on the latest version, one can update from the link below.

Install or upgrade git via the git-scm downloads page.

# Command
```
git --version
```

# Expected Output
```
git version 2.10.1
```

5. Create and Clone a GitHub Repository
Our work on GitHub will be done through the web application interface, however one can easily create a new repository from the terminal. To do so and setup other GitHub related SSH tools, please follow these official steps.

First, log into GitHub (or create an account here) and create a new repository.


How the GitHub new repository form should look
We will add the following fields:

Repository name: modern-django
Description: Modern Django: A Guide on How to Deploy Django-based Web Applications
Visibility as Public
Initialize with a markdown file called README
Add a .gitignore file with standard Python project files that will not get picked up when git checks a directory for changes
Add an MIT License or pick one suitable for your project. Information about different licenses can be found here.
Now that the repository is created, select the ability to clone it and copy the command to the clipboard.

Once the link has been copied (or if you prefer to type it), in a terminal editor navigate to your home directory, create a folder named git (if one does not already exist), move into the git folder, and then git clone the repository. Below are the commands to do so:

Note: The use of the ‘git’ directory name is my personal preference, storing any git projects I have in this directory from multiple services (GitHub, BitBucket, etc). This project can be stored in any directory however. Here is some discussion on using the /srv directory for POSIX systems found here. Your project will almost always be in a different location during production (more on that later).

# Navigate to the home directory with the use of 'cd' and '~' as where to go. '~' represents the current user's home directory.
```
cd ~
```

# Create the git folder, if it already exists no problems will occur with the -p flag
```
mkdir -p git
```

# Knowing that the directory exists, navigate into it
```
cd git
```

# Clone the newly created repository
```
git clone https://github.com/<your_github_user_name>/modern-django.git
```

6. Create a virtualenv and Install Django
Assuming that the repository has been cloned, one can then navigate into it. After ensuring they are in the correct directory, create the file requirements.txt. Then add the latest version of Django to the requirements that pip will install. We will show the addition via the terminal command echo, but one can always make the addition with the text editor of their choice.

# Move into the newly created repository
```
cd ~/git/modern-django/
```

# Create requirements.txt
```
nano requirements.txt
```

# Add Django to the requirements
```
Django==2.2
```

Note: The requirements.txt file is where we will store the dependencies of our project. It is important to always specific a version number for the tool installed, else when recreating the project on another machine, the dependencies may have updated remotely. This will cause major differences between environments.

After setting up the requirements.txt, we will create a virtualenv for our local development Python environment. This will store the Python tools we need to develop our web application, keeping them separate from those accessible by the system.

In the below command, -p allows us to specific a Python executable (our Python 3 instance) and the ‘venv’ portion is the directory our virtualenv will live in.

```
virtualenv -p python3 venv
```
Note: Due to the standard Python .gitignore provided by initializing with GitHub, the venv directory will not be picked up into the project structure when making commits. This is intentional! When moving to another environment you would simply make a new virtualenv with the above commands.

Whenever you would like to go back to the system’s Python environment simply use deactivate. This will remove the (venv) at the beginning of new lines.

# Command
```
deactivate
```

Ensure that the virtualenv is using Python 3 as the default Python.

# Command
```
python --version
```
# Expected Output
```
Python 3.6.0
```

After the virtualenv creation and ensuring the Python executable is version 3.6, it is time to activate the environment and install Django. After activating the virtualenv, you will notice (venv) at the beginning of your terminal input. This helps to denote which environment that terminal instance is using.

Flags for pip install command:

U: stands for upgrade, upgrading any existing packages to their version specified or if no version specified, to the newest available stable build
r: stands for installing all items in the file path given, being the current directories requirements.txt file

# Activate the virtualenv venv
```
source venv/bin/activate
```

# Install Django via pip installing all dependencies in requirements.txt
```
pip install -Ur requirements.txt
```

7. Create a Django Project

# Command
```
django-admin startproject project_name
```

You will see no output, however the config directory, its content, and manage.py have now been created in the modern-django directory. If you use the ls command (summary of ls), you will see the contents of your new Django project, ready to be worked on.

Flags for the ls command:

l: long format, displaying Unix file types, permissions, number of hard links, owner, group, size, last-modified date and filename
a: displays files that start with ‘.’

# Command
```
ls -la
```

# Expected Output
```
total 40
drwxr-xr-x  8 <user>  staff   272 Feb 22 22:03 .
drwxr-xr-x  9 <user>  staff   306 Feb 22 21:37 ..
-rw-r--r--  1 <user>  staff  1045 Feb 22 21:30 .gitignore
-rw-r--r--  1 <user>  staff  1062 Feb 22 21:30 LICENSE
-rw-r--r--  1 <user>  staff    94 Feb 22 21:30 README.md
drwxr-xr-x  6 <user>  staff   204 Feb 22 22:03 config
-rwxr-xr-x  1 <user>  staff   804 Feb 22 22:03 manage.py
-rw-r--r--  1 <user>  staff    15 Feb 22 21:30 requirements.txt
drwxr-xr-x  7 <user>  staff   238 Feb 22 00:30 venv
```

8. Committing and Pushing
Now that the initial project has been created it is time to push it to the remote GitHub repository.

First check which files are different from the remote repository with git status:

# Command
```
git status
```

# Expected Output
```
On branch master
Your branch is up-to-date with 'origin/master'.
Untracked files:
  (use "git add <file>..." to include in what will be committed)
 config/
 manage.py
 requirements.txt
nothing added to commit but untracked files present (use "git add" to track)
Add the directory config, manage.py and the requirements.txt to the tracked files.
```

# Command
```
git add config/ manage.py requirements.txt
```

Use git status again to check which files are now being tracked and need to be committed.

# Command
```
git status
```

# Expected Output
```
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
 new file:   config/__init__.py
 new file:   config/settings.py
 new file:   config/urls.py
 new file:   config/wsgi.py
 new file:   manage.py
 new file:   requirements.txt
```

Now it is time to commit these files. When committing it is important to add a message about the changes made. The —m flag is a shortcut for adding a message during the git commit command.

# Command
```
git commit -m "Initial Project Structure"
```

# Expected Output
```
[master <commit hash>] Initial Project Structure
 6 files changed, 180 insertions(+)
 create mode 100644 config/__init__.py
 create mode 100644 config/settings.py
 create mode 100644 config/urls.py
 create mode 100644 config/wsgi.py
 create mode 100644 manage.py
 create mode 100644 requirements.txt
```

For one last time, do a git status to ensure that your local branch is ahead of master.

# Command
```
git status
```

# Expected Output
```
On branch master
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)
nothing to commit, working tree clean
```

Finally push the changes to your GitHub repository!

Note: You may be prompted for password input if you have not setup your SSH keys and cloned via the SSH URL as described above.

# Command
```
git push
```
# Expected Output
```
Counting objects: 10, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (8/8), done.
Writing objects: 100% (10/10), 2.82 KiB | 0 bytes/s, done.
Total 10 (delta 0), reused 0 (delta 0)
To https://github.com/<your_github_user_name>/modern-django.git
   <hash>..<hash>  master -> master
Congratulations! The initial Django project has been created and pushed to the remote repository. This is a crucial first step for the development of a Modern Django application.
```
