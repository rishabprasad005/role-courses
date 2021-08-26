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

</br></br>

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

</br></br>

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

</br></br>

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

</br></br>

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
  
</br></br>

# **Chapter 6:** Managing Local Users and Groups [IMPORTANT]

## **6.1.** Describing User and Group Concepts

- After completing this section, you should be able to describe the purpose of users and groups on a Linux system.
- Users and groups
- UID and GID
- Primary Groups and Supplementary Groups
- **_/etc/passwd_** and **_/etc/group_** file

## **6.3.** Gaining Superuser Access

- After completing this section, you will be able to switch to the superuser account to manage a Linux system, and grant other users superuser access through the sudo command.
- The Superuser (_root_)
- Switching Users
- Running Commands with Sudo
- Configuring Sudo

## **6.4.** Guided Exercise: Gaining Superuser Access

- In this exercise, you should be able to:-
  - Use sudo to switch to root and access the interactive shell as root without knowing the password of the superuser.
  - Explain how su and su - can affect the shell environment through running or not running the login scripts.
  - Use sudo to run other commands as root.

## **6.5.** Managing Local User Accounts

- After completing this section, you should be able to create, modify, and delete local user accounts.
- Creating Users from the Command Line
- Modifying Existing Users from the Command Line
- Deleting Users from the Command Line
- UID Ranges

## **6.7.** Managing Local Group Accounts

- After completing this section, students should be able to create, modify, and delete local group accounts.
- Creating Groups from the Command Line
- Modifying Existing Groups from the Command Line
- Deleting Groups from the Command Line
- Changing Group Membership from the Command Line

## **6.9.** Managing User Passwords

- After completing this section, you should be able to set a password management policy for users, and manually lock and unlock user accounts.
- Shadow Passwords and Password Policy
  - Format of an Encrypted Password
  - Password Verification
- Configuring Password Aging
- Restricting Access
  - Lock Account
  - Expire Account
  - The noLogin Shell

## **6.10.** Guided Exercise: Managing User Passwords

- In this exercise, you will set password policies for several users.
- You should be able to:-
  - Force a password change when the user logs in to the system for the first time.
  - Force a password change every 90 days.
  - Set the account to expire 180 days from the current day.

## **6.11.** Lab: Managing Local Users and Groups

- In this lab you will set a default local password policy, create a supplementary group for three users, allow that group to use sudo to run commands as root, and modify the password policy for one user.

- You should be able to:-
  - Set a default password aging policy of the local user's password.
  - Create a group and use the group as a supplementary group for new users.
  - Create three new users with the new group as their supplementary group.
  - Configure the group members of the supplementary group to run any command as any user using sudo.
  - Set a user-specific password aging policy.

</br></br>

# **Chapter 7:** Controlling Access to Files

## **7.1.** Interpreting Linux File System Permissions

- After completing this section, you should be able to list file-system permissions on files and directories, and interpret the effect of those permissions on access by users and groups.
- Ownership and Permissions of File and Directory in Linux
- Viewing File and Directory Permissions and Ownership
- Examples of File permissions effect

## **7.3.** Managing File System Permissions from the Command Line

- After completing this section, you should be able to change the permissions and ownership of files using command-line tools.
- Changing File and Directory Permissions
  - Symbolic Method
  - Numeric Method
- Changing File and Directory User or Group Ownership
  - `chown` vs `chgrp`

## **7.4.** Guided Exercise: Managing File System Permissions from the Command Line

- In this exercise, you will use file system permissions to create a directory in which all members of a particular group can add and delete files
- You should be able to create a collaborative directory that is accessible by all members of a particular group

## **7.5.** Managing Default Permissions and File Access

- After completing this section, students should be able to:-
  - Control the default permissions of new files created by users.
  - Explain the effect of special permissions. [SUID, GUID, Sticky Bit]
  - Use special permissions and default permissions to set the group owner of files created in a particular directory.
  - Default permissions for files and directories
  - Learn what is umask and how you can use it to change default permissions

## **7.6.** Guided Exercise: Managing Default Permissions and File Access

- In this exercise, you will control the permissions on new files created in a directory by using umask settings and the setgid permission.
- You also should be able to:-
  - Create a shared directory where new files are automatically owned by the operators group.
  - Experiment with various umask settings.
  - Adjust default permissions for specific users.
  - Confirm your adjustment is correct.

## **7.7.** Lab: Controlling Access to Files

- In this lab, you will configure permissions on files and set up a directory that users in a particular group can use to conveniently share files on the local file system.
- You should be able to:
  - Create a directory where users can work collaboratively on files.
  - Create files that are automatically assigned group ownership.
  - Create files that are not accessible outside of the group.

</br></br>

# **Chapter 8:** Monitoring and Managing Linux Processes

## **8.1.** Listing Processes

- After completing this section, you should be able to get information about programs running on a system to determine status, resource use, and ownership, so you can control them.
- Definition of a Process
- Describing Process States
- Listing Processes using **_ps_** command

## **8.3.** Controlling Jobs

- After completing this section, you should be able to use Bash job control to manage multiple processes started from the same terminal session.
- Describing Jobs and Sessions
- Running Jobs in the Background
- `jobs` command

## **8.4.** Guided Exercise: Controlling Jobs

- In this exercise, you will start, suspend, background, and foreground multiple processes using job control.

## **8.5.** Killing Processes

- After completing this section, you should be able to:
  - Use commands to kill and communicate with processes.
  - Define the characteristics of a daemon process.
  - End user sessions and processes.
- Process control using signals
- Logging Users Out Administratively
- Linux Commands: `kill`, `killall`, `ps`, `w`, `pkill`, `pgrep`, `pstree`)

</br></br>