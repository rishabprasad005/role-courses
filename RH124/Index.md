# **Chapter 1:** Getting Started with Red Hat Enterprise Linux

## **1.1.** What is Linux?

- After completing this section, you should be able to define and explain the purpose of Linux, open source, Linux distributions, and Red Hat Enterprise Linux.
- Why Should You Learn about Linux?
- What Makes Linux Great?
- What is Open Source Software?
- Types of Open Source Licenses
- Who Develops Open Source Software?
- Who is Red Hat?
- What is a Linux distribution?
- Red Hat Enterprise Linux
  - Fedora
  - RHEL
  - CentOS

# **Chapter 2:** Accessing the Command Line

## **2.1.** Accessing the Command Line

- After completing this section, you should be able to log in to a Linux system and run simple commands using the shell.
- Introduction to the Bash Shell (bash vs sh)
- Logging in to a Local Computer
- Logging in to a Remote Server using ssh

## **2.3.** Accessing the Command Line Using the Desktop

- After completing this section, you should be able to log in to the Linux system using the GNOME 3 desktop environment to run commands from a shell prompt in a terminal program.
- Introduction to the GNOME Desktop Environment
- Workspaces
- Starting a Terminal
- Locking the Screen or Logging Out
- Powering off or Rebooting the System

## **2.5.** Executing Commands Using the Bash Shell

- After completing this section, you should be able to save time running commands from a shell prompt using Bash shortcuts
- Basic Command Syntax
- Examples of Simple Commands
  - date, passwd, file, cat, less, head, tail, wc, history

# **Chapter 3:** Managing Files From the Command Line

## **3.1.** Describing Linux File System Hierarchy Concepts

- After completing this section, you should be able to describe:-
  - How Linux organizes files
  - The purposes of various directories in the file-system hierarchy

## **3.3.** Specifying Files by Name

- After completing this section, you should be able to:-
  - Recognize Absolute Paths and Relative Paths
  - Specify the location of files relative to the current working directory and by absolute location
  - Determine and change the working directory
  - List the contents of directories

## **3.5.** Managing Files Using Command-line Tools [IMPORTANT]

- After completing this section, you should be able to create, copy, move, and remove files and directories.

## **3.7.** Making Links Between Files

- After completing this section, you should be able to:-
  - Make multiple file names reference the same file using hard links and symbolic (or "soft") links.
  - Tell the difference between hard link and symbolic link
  - use **df** command to list the directories that are on different file systems

## **3.9.** Matching File Names with Shell Expansions [IMPORTANT]

- After completing this section, you should be able to efficiently run commands affecting many files by using pattern matching features of the Bash shell.
- Command-line Expansions
  - Pattern Matching (globbing)
  - Tilde Expansion
  - Brace Expansion
  - Variable Expansion
  - Command Substitution
- Protecting Arguments from Expansion

## **3.11.** Lab: Managing Files from the Command Line

- In this lab, you will efficiently create, move, and remove files and directories by using the shell and a variety of file name matching techniques.
- You should be able to use wildcards to locate and manipulate files.

# **Chapter 4:** Getting Help in Red Hat Enterprise Linux

## **4.1.** Reading Manual Pages

- After completing this section, you will be able to find information in local Linux system manual pages.
- Introducing the man command
- Navigate and Search Man Pages
- Searching for man pages by keyword

## **4.3.** Reading Info Documentation

- After completing this section, students should be able to find information from local documentation in GNU Info.
- Introducing GNU Info
- Reading Info Documentation
- Comparing GNU Info and Man Page Navigation

# **Chapter 5:** Creating, Viewing, and Editing Text Files [IMPORTANT]

## **5.1.** Redirecting Output to a File or Program

- After completing this section, you should be able to save output or errors to a file with shell redirection, and process command output through multiple command-line programs with pipes. 
- Standard Input, Standard Output, and Standard Error
- Redirecting Standard Output and Standard Error to a File
- I/O Redirection in pipelines (**tee command**)

## **5.3.** Editing Text Files from the Shell Prompt

- After completing this section, you should be able to create and edit text files from the command line using the vim editor.

## **5.5.** Changing the Shell Environment

- After completing this section, you should be able to:-
  - set shell variables to help run commands
  - edit Bash startup scripts (**_/etc/profile_**, **_/etc/bashrc_**, and **_~/.bash_profile_**), to set the shell and environment variables to modify the behavior of the shell and programs run from the shell.

## **5.7.** Lab: Creating, Viewing, and Editing Text Files

- In this lab you will edit a text file, using the vim editor.
- You should be able to:-
  - Use Vim to perform file editing.
  - Use visual mode to simplify file editing. 
  