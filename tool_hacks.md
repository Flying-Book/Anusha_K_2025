---
layout: post
title: Tool Hacks
categories: [Tools]
description: Useful tools for development
permalink: /tools/hacks
---
# Version Control and Deployment

## Version Control

Version control is essential in development for tracking changes, collaborating with others, and managing different versions of your project. Here’s how it works:

**Git Lense:** GitLens for VS Code simplifies Git complexity into a clear, visual timeline of your project's history, helping you track changes and visualize the impact of each commit with ease. You can  quickly glimpse into whom, why, and when a line or code block was changed. 

### Cloning a Repository

To get files from GitHub onto your local machine, use the `git clone` command. This creates a copy of the repository in your chosen directory:
~
git clone <repository_url>
~
Navigating Files
After cloning, navigate to the project directory using the cd 

~~~
cd /path/to/cloned/repository
~~~
Updating Files
To update files on GitHub, use the following commands:
Stage Changes:
~~~
git add .
~~~
Commit Changes:
~~~
git commit -m "Your commit message"
~~~
Push Changes:
~~~
git push
~~~

## Localhost vs. Deployed Server
**Localhost:**
Running your project on localhost means it's only visible on your local machine. The URL is usually http://localhost:4100. Only you can see this version unless you share your screen or expose the port.

**Deployed Server:**
On a deployed server, like GitHub Pages, your project is accessible on the internet.The URL typically looks like https://flying_book.github.io/project, and anyone with the link can view it.

## DNS and GitHub Pages
**Domain:**
GitHub Pages provides a default domain in the format flying_book.github.io/repository-name. You can also set up a custom domain if you have one.

**URL Differences:**
The URL for your GitHub Pages project is unique to your repository. It will differ from others unless you’re working on a shared repository. Changing the repository name or setting up a custom domain will also change the URL.
## Jupyter Kernelspec List
Currently dealing with a problem with the command on jupyter. Instead manually access the list with this command...
~~~
ls /usr/share/jupyter/kernels/
~~~
---
## Shell Script for Version Checks + File Directory
~~~
# Clear the terminal output for a clean start
clear

# Function to check if Ruby is installed
check_ruby() {
  if command -v ruby >/dev/null 2>&1; then
    echo -e "\e[32mRuby is installed: $(ruby -v)\e[0m"
  else
    echo -e "\e[31mRuby is not installed.\e[0m"
  fi
}

# Function to check if Python is installed
check_python() {
  if command -v python3 >/dev/null 2>&1; then
    echo -e "\e[32mPython3 is installed: $(python3 --version)\e[0m"
  elif command -v python >/dev/null 2>&1; then
    echo -e "\e[32mPython is installed: $(python --version)\e[0m"
  else
    echo -e "\e[31mPython is not installed.\e[0m"
  fi
}

# Function to list global git configuration
check_git_config() {
  echo -e "\e[34mGlobal Git configuration:\e[0m"
  git config --global --list
}

# Function to show Git repository details
show_git_repo_details() {
  if [ -d ".git" ]; then
    echo -e "\e[34mGit repository details:\e[0m"
    git remote -v
    git branch
  else
    echo -e "\e[31mThis directory is not a Git repository.\e[0m"
  fi
}

# Function to show current environment variables
show_env_vars() {
  echo -e "\e[34mCurrent environment variables:\e[0m"
  printenv
}

# Function to list the contents of a specific folder within the project
list_folder_contents() {
  local folder="$1/$2"
  if [ -d "$folder" ]; then
    echo -e "\e[34mListing contents of '$2' folder in project directory '$1':\e[0m"
    ls -la "$folder"
    echo "-----------------------------"
  else
    echo -e "\e[31m'$2' folder does not exist in the project directory '$1'.\e[0m"
    echo "-----------------------------"
  fi
}

# Main script execution
echo -e "\e[33mStarting system checks...\e[0m"

# Perform checks for Ruby, Python, Git configuration, and Git repository details
check_ruby
echo "-----------------------------"
check_python
echo "-----------------------------"
check_git_config
echo "-----------------------------"
show_git_repo_details
echo "-----------------------------"

# Show current environment variables
show_env_vars
echo "-----------------------------"

# Prompt for the project directory and list specific folders
echo -e "\e[34mPlease enter the project directory you want to inspect:\e[0m"
read -r project

list_folder_contents "$project" "_notebooks"
list_folder_contents "$project" "_posts"
list_folder_contents "$project" "images"

echo -e "\e[33mSystem checks and folder listing complete.\e[0m"
~~~





