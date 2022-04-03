# **Chapter 1:** Getting Started with Red Hat Enterprise Linux

## **1.1.** What is Linux?

- Benefits of open source software for the user:-
  - Code can survive the loss of the original developer or distributor.
  - You can learn from real-world code and develop more effective applications.

- Following are the ways in which Red Hat develops their products for the future and interacts with the community:-
  - Sponsor and integrate open source projects into the community-driven Fedora project
  - Participate in upstream projects

- Benefits of Linux:-
  - Linux is modular and can be configured as a full graphical desktop or a small appliance
  - Linux includes a powerful and scriptable command-line interface, enabling easier automation and provisioning

## **1.3.** Summary

- Open source software is software with source code that anyone can freely use, study, modify, and share.

- A Linux distribution is an installable operating system constructed from a Linux kernel and supporting user programs and libraries.

- Red Hat participates in supporting and contributing code to open source projects, sponsors and integrates project software into community-driven distributions, and stabilizes the software to offer it as supported enterprise-ready products.

- Red Hat Enterprise Linux is Red Hat's open source, enterprise-ready, commercially-supported Linux distribution.

</br></br>

# **Chapter 2:** Accessing the Command Line

## Difference between **sh** and **bash**:-

- **What is sh?**
  
  Technically speaking, the shell is basically a program that interprets commands typed in by the user in a terminal. However, sh is just the specification for the programming language described by the POSIX standard. It has many implementations (ksh88, dash, ...). bash can also be considered an implementation of sh.

  Since _sh_ is a specification, not an implementation, _/bin/sh_ is a symlink (or a hard link) to an actual implementation on most POSIX systems.

  TODO: How can you find out what /bin/sh points to on your system?

- **What is bash?**

  bash is a programming language that can be thought of as an implementation of sh (although that has changed with time). bash started as an sh-compatible implementation (although it predates the POSIX standard by a few years), but as time passed it has acquired many extensions. Many of these extensions may change the behavior of valid POSIX shell scripts, so by itself bash is not a valid POSIX shell. Rather, it is a dialect of the POSIX shell language.

  bash supports a _--posix_ switch, which makes it more POSIX-compliant. It also tries to mimic POSIX if invoked as sh.

- **sh = bash?**

  For a long time, _/bin/sh_ used to point to _/bin/bash_ on most GNU/Linux systems. As a result, it had almost become safe to ignore the difference between the two. But that started to change recently.

  Some popular examples of systems where _/bin/sh_ does not point to _/bin/bash_ (and on some of which /bin/bash may not even exist) are:-
    - Modern Debian and Ubuntu systems, which symlink sh to dash by default (_/bin/dash)_.
    - Busybox, which is usually run during the Linux system boot time as part of initramfs. It uses the ash shell implementation.
    - Solaris has its own sh which for a long time was not POSIX-compliant

- **Shebang line**

  Ultimately, it's up to you to decide which one to use, by writing the «shebang» line as the very first line of the script.
    - `#!/bin/sh` : will use whatever _sh_ happens to point to
    - `#!/bin/bash` : will use /bin/bash if it's available (and fail with an error message if it's not). 
    - Of course, you can also specify another implementation, e.g. `#!/bin/dash`

- **Which one to use?**

  For my own scripts, I prefer sh for the following reasons:
    - it is standardized
    - it is much simpler and easier to learn
    - it is portable across POSIX systems - even if they happen not to have bash, they are required to have _sh_

  There are advantages to using bash as well. Its features make programming more convenient and similar to programming in other modern programming languages. These include things like scoped local variables and arrays. Plain _sh_ is a very minimalistic programming language.

## **2.1.** Accessing the Command Line

- A command line is a text-based interface which can be used to input instructions to a computer system. **The Linux command line is provided by a program called the shell**. The shell is basically a program that interprets commands typed in by the user.
  
- Various options for the shell program have been developed over the years, and different users can be configured to use different shells. Most users, however, stick with the current default.

- The default shell for users in Red Hat Enterprise Linux is the GNU Bourne-Again Shell (bash). Bash is an improved version of one of the most successful shells used on UNIX-like systems, the Bourne Shell (sh).

- Using bash to execute commands can be powerful. **The bash shell provides a scripting language that can support automation of tasks**. The shell has additional capabilities that can simplify or make possible operations that are hard to accomplish efficiently with graphical tools.

- Shell scripting is scripting in any shell, whereas Bash scripting is scripting specifically for Bash

- When a shell is used interactively, it displays a string when it is waiting for a command from the user. this is called the shell prompt. When a regular user starts a shell, the default prompt ends with a **$** character. The $ character is replaced by a **#** character if the shell is running as the superuser, root. This makes it more obvious that it is a superuser shell, which helps to avoid accidents and mistakes which can affect the whole system.

- To get a shell prompt you must start a terminal program in the graphical environment. The shell prompt is provided in an application window of your graphical terminal program.

- In Linux, the most common way to get a shell prompt on a remote system is to use Secure Shell (SSH). Most Linux systems (including Red Hat Enterprise Linux) and macOS provide the OpenSSH command-line program _'ssh'_ for this purpose.
  
- The ssh command encrypts the connection to secure the communication against eavesdropping or hijacking of the passwords and content.

  Some systems (such as new cloud instances) do not allow users to use a password to log in with ssh for tighter security. An alternative way to authenticate to a remote machine without entering a password is through public key authentication.

  With this authentication method, users have a special identity file containing a private key, which is equivalent to a password, and which they keep secret. Their account on the server is configured with a matching public key, which does not have to be secret. When logging in, users can configure ssh to provide the private key and if their matching public key is installed in that account on that remote server, it will log them in without asking for a password.

- Many system administrators choose not to run a graphical environment on their servers. this allows resources which would be used by the graphical environment to be used by the server's services instead.

- A headless server does not have a keyboard and display permanently connected to it. A data center may be filled with many racks of headless servers, and not providing each with a keyboard and display saves space and expense. To allow administrators to log in, a headless server might have a login prompt provided by its serial console, running on a serial port which is connected to a networked console server for remote access to the serial console.

- The first time you log in to a new machine, you will be prompted with a warning from ssh that it cannot establish the authenticity of the host:

  ```bash
  [user@host ~]$ ssh -i mylab.pem remoteuser@remotehost
  the authenticity of host remotehost (192.0.2.42) cannot be established.
  ECDSA key fingerprint is 47:bf:82:cd:fa:68:06:ee:d8:83:03:1a:bb:29:14:a3.
  Are you sure you want to continue connecting (yes/no)? yes
  ```

   Each time you connect to a remote host with ssh, the remote host sends ssh  its host key to authenticate itself and to help set up encrypted  communication. The ssh command compares that against a list of saved host  keys to make sure it has not changed. If the host key has changed, this  might indicate that someone is trying to pretend to be that host to hijack  the connection which is also known as man-in-the-middle attack. In SSH, host  keys protect against man-in-the-middle attacks, these host keys are unique  for each server, and they need to be changed periodically and whenever a  compromise is suspected.

  You will get this warning if your local machine does not have a host key saved for the remote host. If you enter yes, the host key that the remote host sent will be accepted and saved for future reference. Login will continue, and you should not see this message again when connecting to this host. If you enter no, the host key will be rejected and the connection closed.

  If the local machine does have a host key saved and it does not match the one actually sent by the remote host, the connection will automatically be closed with a warning.

## **2.3.** Accessing the Command Line Using the Desktop

- **What is GNOME?**

GNOME (GNU Network Object Model Environment, pronounced gah-NOHM) is a graphical user interface (GUI) and set of computer desktop applications for users of the Linux operating system. It's intended to make a Linux operating system easy to use for non-programmers and generally corresponds to the Windows desktop interface and its most common set of applications. In fact, GNOME allows the user to select one of several desktop appearances. With GNOME, the user interface can, for example, be made to look like Windows or like Mac OS. In addition, GNOME includes a set of the same type of applications found in Microsoft Office: a word processor, a spreadsheet program, a database manager, a presentation developer, a Web browser and an email program.

- The desktop environment is the graphical user interface on a Linux system. **The default desktop environment in Red Hat Enterprise Linux 8 is provided by GNOME 3**. It provides an integrated desktop for users and a unified development platform on top of a graphical framework provided by either Wayland (by default) or the legacy X Window System.

- GNOME Shell provides the core user interface functions for the GNOME desktop environment. The GNOME Shell application is highly customizable. Red Hat Enterprise Linux 8 defaults GNOME Shell's look and feel to the "Standard" theme, which is used in this section. Red Hat Enterprise Linux 7 defaulted to an alternative theme named "Classic" that was closer to the look and feel of older versions of GNOME. Either theme can be selected persistently at login by clicking the gear icon next to the Sign In button that is available after selecting your account but before entering your password. 

- You can view and edit the GNOME keyboard shortcuts used by your account. Open the system menu on the right side of the top bar. Click the Settings button on the bottom of the menu on the left. In the application window that opens, select Devices → Keyboard from the left pane. The right pane will display your current shortcut settings.

- Workspaces are separate desktop screens that have different application windows. these can be used to organize the working environment by grouping open application windows by task. For example, windows being used to perform a particular system maintenance activity (such as setting up a new remote server) can be grouped in one workspace, while email and other communication applications can be grouped in another workspace.

## **2.8.** Summary

- The Bash shell is a command interpreter that prompts interactive users to specify Linux commands.

- Many commands have a --help option that displays a usage message or screen.

- Using workspaces makes it easier to organize multiple application windows.

- The Activities button located at the upper-left corner of the top bar provides an overview mode that helps a user organize windows and start applications.

- The file command scans the beginning of a file's contents and displays what type it is.

- The head and tail commands display the beginning and end of a file, respectively.

- You can use Tab completion to complete file names when typing them as arguments to commands.

</br></br>

# **Chapter 3:** Managing Files From the Command Line

## **3.1.** Describing Linux File System Hierarchy Concepts

- The **_/_** directory is the root directory at the top of the file-system hierarchy. Subdirectories of / are used for standardized purposes to organize files by type and purpose. This makes it easier to find files. For example, in the root directory, the subdirectory /boot is used for storing files needed to boot the system.

- The following terms help to describe file-system directory contents:-
  - **static content** remains unchanged until explicitly edited or reconfigured.
  - **dynamic** or **variable** content may be modified or appended by active processes.
  - **persistent content** remains after a reboot, like configuration settings.
  - **runtime content** is process- or system-specific content that is deleted by a reboot.

- The following table lists some of the most important directories on the system by name and purpose. For more detailed information, [click here](https://www.tecmint.com/linux-directory-structure-and-important-files-paths-explained/)

  Location | Purpose
  ---------|--------
  /usr  | Installed software, shared libraries, include files, and read-only program data. Important subdirectories include:-<ul><li>**/usr/bin**: User commands.</li><li>**/usr/sbin**: System administration commands</li><li>**/usr/local**: Locally customized software. </li></ul>
  /etc  | Configuration files specific to this system.
  /var  | Variable data specific to this system that should persist between boots. Files that dynamically change, such as databases, cache directories, log files, printer-spooled documents, and website content may be found under /var.
  /run  | Runtime data for processes started since the last boot. This includes process ID files and lock files, among other things. The contents of this directory are recreated on reboot. This directory consolidates /var/run and /var/lock from earlier versions of Red Hat Enterprise Linux.
  /home  | Home directories are where regular users store their personal data and configuration files.
  /root  | Home directory for the administrative superuser, root.
  /tmp  | A world-writable space for temporary files. Files which have not been accessed, changed, or modified for 10 days are deleted from this directory automatically. Another temporary directory exists, /var/tmp, in which files that have not been accessed, changed, or modified in more than 30 days are deleted automatically.
  /boot  | Files needed in order to start the boot process.
  /dev  | Contains special device files that are used by the system to access hardware.

- In Red Hat Enterprise Linux 7 and later, four older directories in / have identical contents to their counterparts located in /usr:
  - /bin and /usr/bin
  - /sbin and /usr/sbin
  - /lib and /usr/lib
  - /lib64 and /usr/lib64

  In earlier versions of Red Hat Enterprise Linux, these were distinct directories containing different sets of files. In Red Hat Enterprise Linux 7 and later, the directories in / are symbolic links to the matching directories in /usr.

## **3.2.** Quiz

- Which directory contains persistent, system-specific configuration data?
  - /etc

- Which directory contains user home directories?
  - /home

- Which directory contains dynamic data, such as for databases and websites?
  - /var

- Which directory is the administrative superuser's home directory?
  - /root

- Which directory contains regular commands and utilities?
  - /usr/bin

- Which directory contains non-persistent process runtime data?
  - /run

- Which directory contains installed software programs and libraries?
  - /usr

## **3.3.** Specifying Files by Name

- **NOTE:** A space character is acceptable as part of a Linux file name. However, spaces are also used by the shell to separate options and arguments on the command line. If you enter a command that includes a file that has a space in its name, the shell can misinterpret the command and assume that you want to start a new file name or other argument at the space.

  It is possible to avoid this by putting file names in quotes. However, if you do not need to use spaces in file names, it can be simpler to simply avoid using them.

- **Absolute Paths:-**
  - An absolute path is a fully qualified name, specifying the files exact location in the file system hierarchy. It begins at the root (/) directory and specifies each subdirectory that must be traversed to reach the specific file.

  - A path name with a forward slash (/) as the first character is an absolute path name. For example, the absolute path name for the system message log file is _/var/log/messages_.

- **Relative Paths:**
  - Absolute path names can be long to type, so files may also be located relative to the current working directory for your shell prompt.
  
  - Like an absolute path, a relative path identifies a unique file, specifying only the path necessary to reach the file from the working directory.

  - Recognizing relative path names follows a simple rule: A path name with anything other than a forward slash as the first character is a relative path name. A user in the _/var_ directory could refer to the message log file relatively as _log/messages_.

- Linux file systems, including, but not limited to, ext4, XFS, GFS2, and GlusterFS, are case-sensitive. Creating _FileCase.txt_ and _filecase.txt_ in the same directory results in two unique files.

  Non-Linux file systems might work differently. For example, VFAT, Microsoft's NTFS, and Apple's HFS+ have case preserving behavior. Although these file systems are not case-sensitive, they do display file names with the original capitalization used when the file was created. therefore, if you tried to make the files in the preceding example on a VFAT file system, both names would be treated as pointing to the same file instead of two different files.

## **3.7.** Making Links Between Files

- It is possible to create multiple names that point to the same file. there are two ways to do this: by creating a hard link to the file, or by creating a soft link (sometimes called a symbolic link) to the file. Each has its advantages and disadvantages.

- **Hard Links:-**
  - Every file starts with a single hard link, from its initial name to the data on the file system. When you create a new hard link to a file, you create another name that points to that same data. The new hard link acts exactly like the original file name. Once created, you cannot tell the difference between the new hard link and the original name of the file.

  - All hard links that reference the same file will have the same link count, access permissions, user and group ownerships, time stamps, and file content. If any of that information is changed using one hard link, all other hard links pointing to the same file will show the new information as well. this is because each hard link points to the same data on the storage device.

  - Even if the original file gets deleted, the contents of the file are still available as long as at least one hard link exists. Data is only deleted from storage when the last hard link is deleted.

  - Hard links have some limitations. Firstly, hard links can only be used with regular files. You cannot use `ln` to create a hard link to a directory or special file.

  - Secondly, hard links can only be used if both files are on the same file system. The file-system hierarchy can be made up of multiple storage devices. Depending on the configuration of your system, when you change into a new directory, that directory and its contents may be stored on a different file system. You can use the **df** command to list the directories that are on different file systems.

- **Soft Links or Symbolic Links:-**
  - One way to compare hard links and soft links that might help you understand how they work:-
    - A hard link directly points to the data on a storage device
    - A soft link points to another name, that points to data on a storage device

  - The `ln -s` command creates a soft link, which is also called a "symbolic link." A soft link is not a regular file, but a special type of file that points to an existing file or directory.

  - Soft links have some advantages over hard links:-
    - they can link two files on different file systems.
    - they can point to a directory or special file, not just a regular file

  - When the original regular file gets deleted, the soft link will still point to the file but the target is gone. A soft link pointing to a missing file is called a "dangling soft link."

  - One side-effect of the dangling soft link is that if you later create a new file with the same name as the deleted file, the soft link will no longer be "dangling" and will point to the new file.

    Hard links do not work like this. If you delete a hard link and then use normal tools (rather than _ln_) to create a new file with the same name, the new file will not be linked to the old file.

  
## **3.9.** Matching File Names with Shell Expansions

- The Bash shell has multiple ways of expanding a command line including pattern matching, home directory expansion, string expansion, and variable substitution. Perhaps the most powerful of these is the path name-matching capability, historically called globbing. The Bash globbing feature, sometimes called “wildcards”, makes managing large numbers of files easier.

- **Pattern Matching:** Globbing is a shell command-parsing operation that expands a wildcard pattern into a list of matching path names. Command-line metacharacters are replaced by the match list prior to command execution. Patterns that do not return matches display the original pattern request as literal text. The following are common metacharacters and pattern classes. 

  | Pattern | Matches |
  --------|--------
  | *  | Any string of zero or more characters. |
  | ?  | Any single character. |
  | [abc...]  | Any one character in the enclosed class (between the square   brackets). |
  | [!abc...]  | Any one character not in the enclosed class. |
  | [^abc...]  | Any one character not in the enclosed class. |
  | [[:alpha:]]  | Any alphabetic character. |
  | [[:lower:]]  | Any lowercase character. |
  | [[:upper:]]  | Any uppercase character. |
  | [[:alnum:]]  | Any alphabetic character or digit. |
  | [[:punct:]]  | Any printable character not a space or alphanumeric. |
  | [[:digit:]]  | Any single digit from 0 to 9. |
  | [[:space:]]  | Any single white space character. this may include tabs, newlines, carriage returns, form feeds, or spaces. |

- **Tilde Expansion:-** 
  - The Bash shell provides some variables that are prefixed with **‘~’** character which is called Tilde Expansions. Tilde expansion is the process of converting these abbreviations to the directory names that they stand for.

  - Tilde(~) expands to the value of **$HOME** variable. If $HOME is not defined, then it expands to the value of the home directory set for the current user defined in **/etc/passwd** file. The _/etc/passwd_ file contains the username, real name, identification information, and basic account information for each user.

    ```bash
    # Tilde(~) expands to the value of $HOME variable 
    [riprasad@localhost]$ echo $HOME
    /home/riprasad

    [riprasad@localhost]$ echo ~
    /home/riprasad

    # Let's change the value of $HOME variable
    [riprasad@localhost]$ export HOME=/sbin

    [riprasad@localhost]$ echo ~
    /sbin

    # Let's unset the $HOME variable
    [riprasad@localhost]$ unset HOME

    # Tilde(~) expands to the value of home directory of the current user defined in /etc/passwd file
    [riprasad@localhost]$ echo ~
    /home/riprasad
    
    # home directory of the 'riprasad' user defined in /etc/passwd file
    [riprasad@localhost]$ cat /etc/passwd | grep "riprasad" | cut -d ":" -f6
    /home/riprasad   

    ```

  - Tilde expansion provides a way to expand the home directory of the current user or the home directory of the given user name.

    Syntax | Description
    -------|-----------
    ~      | Expand to the variable $HOME or home directory of the current user
    ~USER  | Expand to the home directory of the given username

    ```bash
    # Printing home directory of 'root' user
    [riprasad@localhost]$ echo ~root
    /root
    
    # Printing home directory of 'oracle' user
    [riprasad@localhost]$ echo ~oracle
    /home/oracle

    # Checking the current user
    [riprasad@localhost]$ whoami
    riprasad

    # ~ expands to the home directory of current user
    [riprasad@localhost]$ echo ~
    /home/riprasad

    ```

  - The tilde expansion is also used to expand to several specific pathnames:-
    - Home Directories [**~** and **~USER**]
    - Current/previous working directory [**~+** and **~+**]
    - Directories from directory stack [**~+N** and **~-N**]

    For more details, please refer this [link](https://www.thegeekstuff.com/2010/06/bash-tilde-expansion/)

- **Brace Expansion:** Brace expansion is used to generate discretionary strings of characters. Braces contain a comma-separated list of strings, or a sequence expression. The result includes the text preceding or following the brace definition. Brace expansions may be nested, one inside another. Also double-dot syntax (..) expands to a sequence such that {m..p} will expand to m n o p.

  ```bash
  [user@host glob]$ echo {Sunday,Monday,Tuesday,Wednesday}.log
  Sunday.log Monday.log Tuesday.log Wednesday.log

  [user@host glob]$ echo file{1..3}.txt
  file1.txt file2.txt file3.txt

  [user@host glob]$ echo file{a..c}.txt
  filea.txt fileb.txt filec.txt

  [user@host glob]$ echo file{a,b}{1,2}.txt
  filea1.txt filea2.txt fileb1.txt fileb2.txt

  [user@host glob]$ echo file{a{1,2},b,c}.txt
  filea1.txt filea2.txt fileb.txt filec.txt

  # A practical use of brace expansion is to quickly create a number of files or directories. 
  [user@host glob]$ mkdir RHEL{6,7,8}
  [user@host glob]$ ls RHEL*
  RHEL6 RHEL7 RHEL8
  ```

- **Variable Expansion:** A variable acts like a named container that can store a value in memory. Variables make it easy to access and modify the stored data either from the command line or within a shell script.

  ```bash
  # You can assign data as a value to a variable using the following syntax
  [user@host ~]$ USERNAME=operator
  
  # You can use variable expansion to convert the variable name to its value on the command line
  [user@host ~]$ echo $USERNAME
  operator
  
  #To help avoid mistakes due to other shell expansions, you can put the name of the variable in curly braces,
  [user@host ~]$ echo ${USERNAME}
  operator
  ```

- **Command Substitution:** Command substitution allows the output of a command to replace the command itself on the command line. Command substitution occurs when a command is enclosed in parentheses, and preceded by a dollar sign ($).

  An older form of command substitution uses backticks: \`_command_`. Disadvantages to the backticks form include: 
  - You can visually confuse backticks with single quote marks
  - It has a more complicated and intrusive quoting mechanism


  ```bash
  [user@host glob]$ echo the time is $(date +%M) minutes past $(date +%l%p).
  the time is 26 minutes past 11AM.

  # with backtick
  [user@host glob]$ echo the time is `date +%M` minutes past `date +%l%p`.
  the time is 26 minutes past 11AM.

  # the $(command) form can nest multiple command expansions inside each other.
  [user@host glob]$ echo top $(echo 0 $(echo 1 $(echo 2 $(echo 3))))
  top 0 1 2 3

  # now with backticks
  [user@host glob]$ echo top `echo 0 \`echo 1 \\\`echo 2 \\\\\\\`echo 3\\\\\\\`\\\`\``
  top 0 1 2 3
  ```

- **Protecting Arguments from Expansion:-**
  - Many characters have special meaning in the Bash shell. To keep the shell from performing shell expansions on parts of your command line, you can quote and escape characters and strings.

  - The backslash (\\) is an escape character in the Bash shell. It will protect the character immediately following it from expansion. In the below example, protecting the dollar sign from expansion caused Bash to treat it as a regular character and it did not perform variable expansion on $HOME.

    ```bash
    [user@host glob]$ echo the value of $HOME is your home directory.
    the value of /home/user is your home directory.

    [user@host glob]$ echo the value of \$HOME is your home directory.
    the value of $HOME is your home directory.
    ```

  - To protect longer character strings, single quotes (') or double quotes (") are used to enclose strings. they have slightly different effects. **Single quotes stop all shell expansion. Double quotes stop most shell expansion.**
  
    Use double quotation marks to suppress globbing and shell expansion, but still allow command and variable substitution.

    ```bash
    [user@host glob]$ myhost=$(hostname -s); echo $myhost
    host

    [user@host glob]$ echo "***** hostname is ${myhost} *****"
    ***** hostname is host *****
    ```

    Use single quotation marks to interpret all text literally.

    ```bash
    [user@host glob]$ echo "Will variable $myhost evaluate to $(hostname -s)?"
    Will variable host evaluate to host?

    [user@host glob]$ echo 'Will variable $myhost evaluate to $(hostname -s)?'
    Will variable $myhost evaluate to $(hostname -s)?
    ```

## **3.12.** Summary

- Files on a Linux system are organized into a single inverted tree of directories, known as a file-system hierarchy.
- Absolute paths start with a / and specify the location of a file in the file-system hierarchy.
- Relative paths do not start with a / and specify the location of a file relative to the current working directory.
- Five key commands are used to manage files: mkdir, rmdir, cp, mv, and rm.
- Hard links and soft links are different ways to have multiple file names point to the same data.
- The Bash shell provides pattern matching, expansion, and substitution features to help you efficiently run commands

</br></br>

# **Chapter 5:** Creating, Viewing, and Editing Text Files

## **5.1.** Redirecting Output to a File or Program

### Standard Input, Standard Output, and Standard Error

- A running program, or process, needs to read input from somewhere and write output to somewhere. A command run from the shell prompt normally reads its input from the keyboard and sends its output to its terminal window.

- A process uses numbered channels called file descriptors to get input and send output. All processes start with at least three file descriptors:-
  - **channel 0** : Standard input reads input from the keyboard.
  - **channel 1** : Standard output sends normal output to the terminal.
  - **channel 2** : Standard error sends error messages to the terminal.

  If a program opens separate connections to other files, it may use higher-numbered file descriptors.

- Channels (File Descriptors):-

  Number | Channel name | Description | Default connection | Usage
  -------|--------------|-------------|--------------------|------
  0 | stdin | Standard input | Keyboard | read only
  1 | stdout | Standard output | Terminal | write only
  2 | stderr | Standard error | Terminal | write only
  3+ | filename | Other files | none | read and/or write


### Redirecting Standard Output and Standard Error to a File

- I/O redirection changes how the process gets its input or output. Instead of getting input from the keyboard, or sending output and errors to the terminal, the process reads from or writes to files. Redirection lets you save messages to a file that are normally sent to the terminal window. Alternatively, you can use redirection to discard output or errors, so they are not displayed on the terminal or saved.

- Redirecting stdout suppresses process output from appearing on the terminal. One thing to keep in mind is that redirecting only stdout does not suppress stderr error messages from displaying on the terminal. If you want to discard messages, the special file _/dev/null_ quietly discards channel output redirected to it and is always an empty file.

- If the file storing the output does not exist, it will be created. If the file does exist and the redirection is not the one that appends to the file(> filename), the file's contents will be overwritten. use redirection '>> filename' to append the output to the file.

- Output Redirection Operators:-
    
    <table>
        <tr>
                     <th> Redirection </ th> 
                     <th> Explanation </ th> 
       </tr>
        <tr>
                     <td> $ command > file (or) $ command 1> file </ td> 
                     <td> redirect stdout to overwrite a file </ td> 
       </tr>
        <tr>
                     <td> $ command >> file (or) $ command 1>> file</ td> 
                     <td> redirect stdout to append to a file </ td> 
       </tr>
        <tr>
                     <td> $ command 2> file </ td> 
                     <td> redirect stderr to overwrite a file </ td> 
       </tr>
        <tr>
                     <td> $ command 2> /dev/null </ td> 
                     <td> discard stderr error messages by redirecting to /dev/null </ td> 
       </tr>
        <tr>
                     <td> $ command > file  2>&1 </ td> 
                     <td rowspan = "3"> redirect stdout and stderr to overwrite the same file. <br> [See below for what `&1` and `&2` means </ td> 
       </tr>
       <tr>
                     <td> $ command 1> file  2>&1 </ td> 
       </tr>
        <tr>
                     <td> $ command &> file </ td> 
       </tr>
        <tr>
                     <td> $ command >> file  2>&1 </ td> 
                     <td rowspan = "3"> redirect stdout and stderr to append to the same file </ td> 
       </tr>
       <tr>
                     <td> $ command 1>> file  2>&1 </ td> 
       </tr>
        <tr>
                     <td> $ command &>> file </ td> 
       </tr>
    </table>

- The order of redirection operations is important. The following sequence redirects standard output to file and then redirects standard error to the same place as standard output (file).

  ```bash
   $ command > file 2>&1
  ``` 

  However, the next sequence does redirection in the opposite order. This redirects standard error to the default place for standard output (the terminal window, so no change) and then redirects only standard output to file.

  ```bash
  $ command 2>&1 > file
  ``` 

  Because of this, some people prefer to use the merging redirection operators:-
  - `&>file`	instead of	`>file 2>&1`
  - `&>>file`	instead of	`>>file 2>&1` (in Bash 4 / RHEL 6 and later)

  However, other system administrators and programmers who also use other shells related to bash (known as Bourne-compatible shells) for scripting commands think that the newer merging redirection operators should be avoided, because they are not standardized or implemented in all of those shells and have other limitations.

### Pipelines, Redirection and the 'tee' Command

- A pipeline is a sequence of one or more commands separated by the pipe character `|`. A pipe connects the standard output of the first command to the standard input of the next command. 
  
- Pipelines allow the output of a process to be manipulated and formatted by other processes before it is output to the terminal. One useful mental image is to imagine that data is "flowing" through the pipeline from one process to another, being altered slightly by each command in the pipeline through which it flows.

- Pipelines and I/O redirection both manipulate standard output and standard input. Redirection sends standard output to files or gets standard input from files. Pipes send the standard output from one process to the standard input of another process.

- When redirection is combined with a pipeline, the shell sets up the entire pipeline first, then it redirects input/output. If output redirection is used in the middle of a pipeline, the output will go to the file and not to the next command in the pipeline. In this example, the output of the ls command goes to the file, and less displays nothing on the terminal:-

  ```bash
  [user@host ~]$ ls > /tmp/saved-output | less
  ```

- The tee command overcomes this limitation. In a pipeline, tee copies its standard input to its standard output and also redirects its standard output to the files named as arguments to the command. If you imagine data as water flowing through a pipeline, tee can be visualized as a "T" joint in the pipe which directs output in two directions.

  This example redirects the output of the ls command to the file and passes it to less to be displayed on the terminal one screen at a time.

  ```bash
   [user@host ~]$ ls -l | tee /tmp/saved-output | less
  ```

  If tee is used at the end of a pipeline, then the final output of a command can be saved and output to the terminal at the same time.
  
  ```bash
  [user@host ~]$ ls -t | head -n 10 | tee /tmp/ten-last-changed-files
  ```

- Standard error can be redirected through a pipe, but the merging redirection operators (&> and &>>) cannot be used to do this. The following is the correct way to redirect both standard output and standard error through a pipe:-

  ```bash
  [user@host ~]$ find -name / passwd 2>&1 | less
  ```

## **5.4.** Changing the Shell Environment

### Shell Variables

- The Bash shell allows you to set shell variables that you can use to help run commands or to modify the behavior of the shell. You can use variables to help make it easier to run a command with a long argument, or to apply a common setting to commands run from that shell.
  
- You can also export shell variables as environment variables, which are automatically copied to programs run from that shell when they start.

- Shell variables are unique to a particular shell session. If you have two terminal windows open, or two independent login sessions to the same remote server, you are running two shells. Each shell has its own set of values for its shell variables.

- You can use the **_set_** command to list all shell variables that are currently set. (It also lists all shell functions, which you can ignore.) This list is long enough that you may want to pipe the output into the less command so that you can view it one page at a time.

  ```bash
  [user@host ~]$ set | less
  BASH=/usr/bin/bash
  BASHRCSOURCED=Y
  ...output omitted...
  ```

- If there are any trailing characters adjacent to the variable name, you might need to protect the variable name with curly braces.

  ```bash
  [user@host ~]$ echo Repeat $COUNTx
  Repeat

  [user@host ~]$ echo Repeat ${COUNT}x
  Repeat 40x
  ```

### Configuring Bash with Shell Variables

Some shell variables are set when Bash starts but can be modified to adjust the shell's behavior. For example:-
  
- Two shell variables that affect the shell history and the history command are HISTFILE and HISTFILESIZE. If HISTFILE is set, it specifies the location of a file to save the shell history in when it exits. By default this is the user's ~/.bash_history file. The HISTFILESIZE variable specifies how many commands should be saved in that file from the history.

- Another example is PS1, which is a shell variable that controls the appearance of the shell prompt. If you change this value, it will change the appearance of your shell prompt.

    ```bash
    [user@host ~]$ PS1="[abc]\$ "
    [abc]$

    # reverting the changes
    [abc]$ PS1="[\u@\h \W]\$ "
    [user@host ~]$ 

    ```

### Shell Variables vs Environment Variables

When you create a new variable like SOME_ENV_VARIABLE="testing.txt" it resides in the SHELL scope, that means it can be accessed by that instance of shell where the user is logged in. When the instance change for example you open a new terminal or you change the shell (for example you switch to csh) you can not access that variable.

When you export that variable like export SOME_ENV_VARIABLE that variable is now available in environment scope, that means in that instance if you change the shell you can still access that variable. Lets try to understand with following example:

   ```bash
   [vishrant@localhost]$ SOME_SHELL_VARIABLE="testing.txt" #creating variable in bash shell
   [vishrant@localhost]$ echo $SOME_ENV_VARIABLE
   testing.txt
   [vishrant@localhost]$ csh #changing shell
   [vishrant@localhost ~/shell_scripting]$ echo $SOME_SHELL_VARIABLE
   SOME_SHELL_VARIABLE: Undefined variable.

   # Let's try again
   [vishrant@localhost]$ SOME_ENV_VARIABLE="hello.txt"
   [vishrant@localhost]$ export SOME_ENV_VARIABLE #variable now available with environment
   [vishrant@localhost]$ env | grep SOME_ENV_VARIABLE
   SOME_ENV_VARIABLE=testing.txt
   [vishrant@localhost]$ csh #changing shell
   [vishrant@localhost ~/shell_scripting]$ echo $SOME_ENV_VARIABLE
   testing.txt
   [vishrant@localhost ~/shell_scripting]$ exit
   exit #returned to parent shell
   [vishrant@localhost]$ echo $SOME_ENV_VARIABLE
   SOME_ENV_VARIABLE=testing.txt
   ```

**Analogy**: let's assume you have a two-bedroom apartment and you are sharing it with another roommate. The common area can be accessed by anyone but not your bedrooms, environment variable is like common area and shell variable is like bedroom, if you will something in common area it can be accessed by anyone but if you keep it in your bedroom it can only be accessed by you.

Remember if open a new terminal you won't be able to access either of the variables because you are changing that instance. For that you should add your variables in either .profile or .bashrc (if you are using bash). Opening a new terminal is similar to buying another apartment in the same building. Now again, whatever items are available in the first flat, be it in the common area or bedroom, will not be accessible in the second flat. Now, .profile or .bashrc is like common area of the building like park, gym, swimming pool etc and all the people of the building will have access to it.

### Configuring Programs with Environment Variables

- The shell provides an environment to the programs you run from that shell. This environment includes:-
  - information on the current working directory on the file system
  - The command-line options passed to the program
  - The values of environment variables.

- Shell variables that are not environment variables can only be used by the shell. Environment variables can be used by the shell and by programs run from that shell.

- You can make any variable defined in the shell into an environment variable by marking it for export with the export command.

    ```bash
    [user@host ~]$ EDITOR=vim
    [user@host ~]$ export EDITOR

    # You can set and export a variable in one step:
    [user@host ~]$ export EDITOR=vim
    ```

- By convention, environment variables and shell variables that are automatically set by the shell have names that use all uppercase characters. If you are setting your own variables, you may want to use names made up of lowercase characters to help avoid naming collisions. To list all the environment variables for a particular shell, run the `env` command.

- Applications and sessions use these variables to determine their behavior or their default settings.For example:-
  
  - The shell automatically sets the HOME variable to the file name of the user's home directory when it starts. This can be used to help programs determine where to save files.
  
  - The EDITOR environment variable specifies the program you want to use as your default text editor for command-line programs. Many programs use vi or vim if it is not specified, but you can override this preference if required:-

    ```bash
    [user@host ~]$ export EDITOR=nano
    ```
  
  - Another example is LANG, which sets the locale. This adjusts the preferred language for program output; the character set; the formatting of dates, numbers, and currency; and the sort order for programs. If it is set to en_US.UTF-8, the locale will use US English with UTF-8 Unicode character encoding. If it is set to something else, for example fr_FR.UTF-8, it will use French UTF-8 Unicode encoding.

    ```bash
    [user@host ~]$ date
    Tue Jan 22 16:37:45 CST 2019

    [user@host ~]$ export LANG=fr_FR.UTF-8
    [user@host ~]$ date
    mar. janv. 22 16:38:14 CST 2019
    ```

  - Another important environment variable is PATH. The PATH variable contains a list of colon-separated directories that contain programs:

    ```bash
    [user@host ~]$ echo $PATH
    /home/user/:/home/user/bin:/usr/share/Modules/bin:/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin
    ```

    When you run a command such as ls, the shell looks for the executable file ls in each of those directories in order, and runs the first matching file it finds. (On a typical system, this is /usr/bin/ls.)

    You can easily add additional directories to the end of your PATH. For example, perhaps you have executable programs or scripts that you want to run like regular commands in /home/user/sbin. You can add /home/user/sbin to the end of your PATH for the current session like this:-

    ```bash
    [user@host ~]$ export PATH=${PATH}:/home/user/sbin
    ```

### Setting Variables Automatically

- If you want to set the shell or environment variables automatically, when your shell starts, you can edit the Bash startup scripts. When Bash starts, several text files containing shell commands are run which initialize the shell environment.

- The exact scripts that run depend on how the shell was started, whether it is an interactive login shell, an interactive non-login shell, or a shell script. 
  
- For more details on the execution order of scripts, click [here](https://how-to.fandom.com/wiki/How_to_configure_bash_startup_scripts)

- For more details on different startup scripts(**_/etc/profile_**, **_/etc/bashrc_**, **_~/.bash_profile_** etc), click [here](http://howtolamp.com/articles/bash-startup-scripts/)

- If you want to make a change to your user account that affects all your interactive shell prompts at startup, edit your ~/.bashrc file.

- The best way to adjust settings that affect all user accounts is by adding a file with a name ending in .sh containing the changes to the _/etc/profile.d_ directory. To do this, you need to be logged in as the root user.

### Unsetting and Unexporting Variables

- To unset and unexport a variable entirely, use the unset command:

  ```bash
  [user@host ~]$ echo $file1
  /tmp/tmp.z9pXW0HqcC
  [user@host ~]$ unset file1
  [user@host ~]$ echo $file1
  
  [user@host ~]$
  ``` 

- To unexport a variable without unsetting it, use the export -n command:

  ```bash
  [user@host ~]$ export -n PS1
  ```

## **5.8.** Summary

- Running programs, or processes, have three standard communication channels, standard input, standard output, and standard error.

- You can use I/O redirection to read standard input from a file or write the output or errors from a process to a file.

- Pipelines can be used to connect standard output from one process to standard input of another process, and can be used to format output or build complex commands.

- You should know how to use at least one command-line text editor, and Vim is generally installed.

- Shell variables can help you run commands and are unique to a particular shell session.

- Environment variables can help you configure the behavior of the shell or the processes it starts. 

</br></br>

# **Chapter 6:** Managing Local Users and Groups

## **6.1.** Describing User and Group Concepts

### What is a User?

- A user account is used to provide security boundaries between different people and programs that can run commands.

- Users have user names to identify them to human users and make them easier to work with. Internally, the system distinguishes user accounts by the unique identification number assigned to them, the user ID or UID. In short, internally the operating system uses the UIDs to track users

- User accounts are fundamental to system security. Every process (running program) on the system runs as a particular user. Every file has a particular user as its owner. File ownership helps the system enforce access control for users of the files. The user associated with a running process determines the files and directories accessible to that process.

- There are three main types of user account:-

  - **superuser:** The superuser account is for administration of the system. The name of the superuser is root and the account has UID 0. The superuser has full access to the system.

  - **system users:** The system has system user accounts which are used by processes that provide supporting services. These processes, or daemons, usually do not need to run as the superuser. They are assiged non-privileged accounts that allow them to secure their files and other resources from each other and from regular users on the system. Users do not interactively log in using a system user account.

  - **regular users:** Most users have regular user accounts which they use for their day-to-day work. Like system users, regular users have limited access to the system.

- Some useful Commands:-

   ```bash
   # show information about the currently logged-in user
   [user01@host ~]$ id
   uid=1000(user01) gid=1000(user01) groups=1000(user01) context=unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023

   # To view basic information about another user
   [user01@host]$ id user02
   uid=1002(user02) gid=1001(user02) groups=1001(user02) context=unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023

   # To view process information, use the ps command.
   # Add the _a_ option to view all processes with a terminal.
   # To view the user associated with a process, include the _u_ option.
   [user01@host]$ ps -au
  USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
  root       777  0.0  0.0 225752  1496 tty1     Ss+  11:03   0:00 /sbin/agetty -o -p -- \u --noclear tty1 linux
  root       780  0.0  0.1 225392  2064 ttyS0    Ss+  11:03   0:00 /sbin/agetty -o -p -- \u --keep-baud 115200,38400,9600
  user01      1207  0.0  0.2 234044  5104 pts/0    Ss   11:09   0:00 -bash
  user01      1319  0.0  0.2 266904  3876 pts/0    R+   11:33   0:00 ps au
   ```

- The mapping of usernames to UIDs is defined in databases of account information. By default, systems use the _/etc/passwd_ file to store information about local users. Each line in the _/etc/passwd_ file contains information about one user. It is divided up into seven colon-separated fields. Here is an example of a line from _/etc/passwd_:-

  ```bash
     1     2     3      4        5           6            7
  user01 : x : 1000 : 1000 : User One : /home/user01 : /bin/bash
  ```

  - **1** : Username for this user (user01).
  - **2** : The user's password used to be stored here in encrypted format. That has been moved to the /etc/shadow file, which will be covered later. This field should always be x.
  - **3** : The UID number for this user account (1000).
  - **4** : The GID number for this user account's primary group (1000)
  - **5** : The real name for this user (User One).
  - **6** : The home directory for this user (/home/user01).
  - **7** : The default shell program for this user, which runs on login (/bin/bash). For a regular user, this is normally the program that provides the user's command-line prompt. A system user might use _/sbin/nologin_ if interactive logins are not allowed for that user.

### What is a Group?

- A group is a collection of users that need to share access to files and other system resources. Groups can be used to grant access to files to a set of users instead of just a single user.

- Like users, groups have group names to make them easier to work with. Internally, the system distinguishes groups by the unique identification number assigned to them, the group ID or GID.

- The mapping of group names to GIDs is defined in databases of group account information. By default, systems use the /etc/group file to store information about local groups. Each line in the _/etc/group_ file contains information about one group. Each group entry is divided into four colon-separated fields. Here is an example of a line from _/etc/group_:-

  ```bash
     1      2     3               4
  group01 : x : 10000 : user01,user02,user03
  ```

  - **1** : Group name for this group (group01).
  - **2** : Obsolete group password field. This field should always be x.
  - **3** : The GID number for this group (10000).
  - **4** : A list of users who are members of this group as a supplementary group (user01, user02, user03). Primary (or default) and supplementary groups are discussed later in this section.

- **Primary Groups and Supplementary Groups**:-

  - Every user has exactly one primary group. For local users, this is the group listed by GID number in the _/etc/passwd_ file. By default, this is the group that will own new files created by the user.

  - Normally, when you create a new regular user, a new group with the same name as that user is created. That group is used as the primary group for the new user, and that user is the only member of this User Private Group. It turns out that this helps make management of file permissions simpler, which will be discussed later in this course.

  - Users may also have supplementary groups. Membership in supplementary groups is determined by the /etc/group file. Users are granted access to files based on whether any of their groups have access. It doesn't matter if the group or groups that have access are primary or supplementary for the user.

    For example, if the user user01 has a primary group user01 and supplementary groups wheel and webadmin, then that user can read files readable by any of those three groups.

  - The id command can also be used to find out about group membership for a user.

      ```bash
      [user03@host ~]$ id
      uid=1003(user03) gid=1003(user03) groups=1003(user03),10(wheel),10000(group01) context=unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023
      ```

    In the preceding example, **user03** has the group **user03** as their primary group (gid). The groups item lists all groups for this user. Other than the primary group **user03**, the user has groups **wheel** and **group01** as supplementary groups.

## **6.3.** Gaining Superuser Access

### Super User

- Most operating systems have some sort of superuser, a user that has all power over the system. In Red Hat Enterprise Linux this is the **root** user. This user has the power to override normal privileges on the file system, and is used to manage and administer the system. To perform tasks such as installing or removing software and to manage system files and directories, users must escalate their privileges to the root user.

- The root user only among normal users can control most devices, but there are a few exceptions. For example, normal users can control removable devices, such as USB devices. Thus, normal users can add and remove files and otherwise manage a removable device, but only root can manage "fixed" hard drives by default.

- This unlimited privilege, however, comes with responsibility. The root user has unlimited power to damage the system: remove files and directories, remove user accounts, add back doors, and so on. If the root user's account is compromised, someone else would have administrative control of the system. Throughout this course, administrators are encouraged to log in as a normal user and escalate privileges to root only when needed.
  
- Red Hat recommends that system administrators do not log in directly as root. Instead, system administrators should log in as a normal user and use other mechanisms (su, sudo, or PolicyKit, for example) to temporarily gain superuser privileges.

  By logging in as the superuser, the entire desktop environment unnecessarily runs with administrative privileges. In that situation, any security vulnerability which would normally only compromise the user account has the potential to compromise the entire system.

### Switching Users

- The _su_ command (**S**witch **U**ser) allows users to switch to a different user account.

    ```bash
    [user01@host ~]$ su - user02
    Password: 
    [user02@host ~]$
    ``` 

- If you omit the user name, the **_su_** or **_su -_** command attempts to switch to root by default.

    ```bash
    [user01@host ~]$ su -
    Password: 
    [root@host ~]#
    ``` 

- The command **su** starts a non-login shell, while the command **su -** (with the dash option) starts a login shell. The main distinction between the two commands is that **su -** sets up the shell environment as if it were a new login as that user, while **su** just starts a shell as that user, but uses the original user's environment settings.

  In most cases, administrators should run **su -** to get a shell with the target user's normal environment settings. For more information, see the bash(1) man page.

  For more detailed explanation, <br>
  **sudo** vs **su**  and how to grant sudo priviledges: please click [here](https://www.tecmint.com/su-vs-sudo-and-how-to-configure-sudo-in-linux/)<br>
  **su** vs **su -** : please click [here](https://www.tecmint.com/difference-between-su-and-su-commands-in-linux/)


### Running Commands with Sudo

- In some cases, the root user's account may not have a valid password at all for security reasons. In this case, users cannot log in to the system as root directly with a password, and su cannot be used to get an interactive shell. One tool that can be used to get root access in this case is sudo.

- `su` Vs `sudo` : If a normal user needs to perform any system wide changes he needs to use either ‘su‘ or ‘sudo‘ command. ‘su‘ forces you to share your root password to other users whereas ‘sudo‘ makes it possible to execute system commands without root password. ‘sudo‘ lets you use your own password to execute system commands i.e., delegates system responsibility without root password.

- Unlike su, sudo normally requires users to enter their own password for authentication, not the password of the user account they are trying to access. That is, users who use sudo to run commands as root do not need to know the root password. Instead, they use their own passwords to authenticate access.

- Additionally, sudo can be configured to allow specific users to run any command as some other user, or only some commands as that user. For example, when sudo is configured to allow the _user01_ user to run the command _usermod_ as _root_, _user01_ could run the _usermod_ command to lock or unlock a user account.

- One additional benefit to using sudo is that all commands executed are logged by default to /var/log/secure.

- If a user tries to run a command as another user, and the sudo configuration does not permit it, the command will be blocked, the attempt will be logged, and by default an email will be sent to the root user.

- **Note:** In RHEL-7 and RHEL-8, all members of the **wheel group** can use sudo to run commands as any user, including root. This is a change from RHEL-6 and earlier, where users who were members of the wheel group did not get this administrative access by default.

### Getting an Interactive Root Shell with Sudo

- If there is a nonadministrative user account on the system that can use _sudo_ to run the _su_ command, you can run `sudo su -` from that account to get an interactive root user shell. This works because sudo will run `su -` as _root_, and _root_ does not need to enter a password to use su.

- Another way to access the root account with _sudo_ is to use the `sudo -i` command. This will switch to the _root_ account and run that user's default shell (usually bash) and associated shell login scripts. If you just want to run the shell, you can use the `sudo -s` command.

- For example, an administrator might get an interactive shell as _root_ on an AWS EC2 instance by using SSH public-key authentication to log in as the normal user ec2-user, and then by running `sudo -i` to get the _root_ user's shell.

  ```bash
  [ec2-user@host ~]$ sudo -i
  [sudo] password for ec2-user:
  [root@host ~]#
  ```

- The `sudo su -` command and `sudo -i` do not behave exactly the same. Please check out the course page for more details. The Lab for this sections explains the difference practically.

- Checkout [this](https://askubuntu.com/questions/376199/sudo-su-vs-sudo-i-vs-sudo-bin-bash-when-does-it-matter-which-is-used) explanation as well for more clarity.


### Configuring Sudo

- The main configuration file for sudo is _/etc/sudoers_. To avoid problems if multiple administrators try to edit it at the same time, it should only be edited with the special `visudo` command.

- The Syntax of configured ‘sudo‘ line is:
  
  ```bash
  User_name Machine_name=(Effective_user) command
  ```

  The above Syntax can be divided into four parts:-
    - **User_name**: This is the name of ‘sudo‘ user.
    - **Machine_name**: This is the host name, in which ‘sudo‘ command is valid. Useful when you have lots of host machines.
    - **(Effective_user)**: The ‘Effective user’ that are allowed to execute the commands. This column lets you allows users to execute System Commands.
    - **Command**: command or a set of commands which user may run.


- For example, the following line from the _/etc/sudoers_ file enables sudo access for members of group _wheel_.

  ```bash
  %wheel        ALL=(ALL)       ALL
  ```

  In this line, **_%wheel_** is the user or group to whom the rule applies. A % specifies that this is a group. The _**ALL=(ALL)**_ specifies that on any host that might have this file, _wheel_ can run any command. The final **_ALL_** specifies that wheel can run those commands as any user on the system.

  Multiple examples for the corressponding sudo lines for users, where you need to grant sudo privileges for different use-cases can be found [here](https://www.tecmint.com/su-vs-sudo-and-how-to-configure-sudo-in-linux/)

- By default, _/etc/sudoers_ also includes the contents of any files present in the **_/etc/sudoers.d_** directory as part of the configuration file. This allows an administrator to add sudo access for a user simply by putting an appropriate file in that directory. Using supplementary files under the _/etc/sudoers.d_ directory is convenient and simple. You can enable or disable sudo access simply by copying a file into the directory or removing it from the directory.

- To enable full sudo access for the user user01, you could create /etc/sudoers.d/user01 with the following content:

  ```bash
  user01  ALL=(ALL)  ALL
  ```

  To enable full sudo access for the group group01, you could create /etc/sudoers.d/group01 with the following content:

  ```bash
  %group01  ALL=(ALL)  ALL
  ```

   It is also possible to set up sudo to allow a user to run commands as another user without entering their password:

   ```bash
   ansible  ALL=(ALL)  NOPASSWD:ALL
   ```

   While there are obvious security risks to granting this level of access to a user or group, it is frequently used with cloud instances, virtual machines, and provisioning systems to help configure servers. The account with this access must be carefully protected and might require SSH public-key authentication in order for a user on a remote system to access it at all.

## **6.5** - **6.7:** Managing Local User Accounts && Groups

- Refer to the tutorial for CLI commands used to add, delete and manage local user accounts and groups.

- **UID Ranges:** Specific UID numbers and ranges of numbers are used for specific purposes by Red Hat Enterprise Linux.
  - **UID 0** is always assigned to the superuser account, **root**.
  
  - **UID 1-200** is a range of "**system users**" assigned statically to system processes by Red Hat.
  
  - **UID 201-999** is a range of "system users" used by system processes that do not own files on the file system. They are typically assigned dynamically from the available pool when the software that needs them is installed. Programs run as these "unprivileged" system users in order to limit their access to only the resources they need to function.

  - **UID 1000+** is the range available for assignment to **regular users**.

  **Note:** Prior to RHEL 7, the convention was that UID 1-499 was used for system users and UID 500+ for regular users. Default ranges used by useradd and groupadd can be changed in the /etc/login.defs file.

- GID Range is similar to the UID Range. Hence, the UID and GID of a new user usually are the same.
  
   **Note:** Given the automatic creation of user private groups (GID 1000+), it is generally recommended to set aside a range of GIDs to be used for supplementary groups. A higher range will avoid a collision with a system group (GID 0-999).

## **6.9.** Managing User Passwords

### Shadow Passwords and Password Policy

- At one time, encrypted passwords were stored in the world-readable _/etc/passwd_ file. This was thought to be reasonably secure until dictionary attacks on encrypted passwords became common. At that point, the encrypted passwords were moved to a separate _/etc/shadow_ file which is readable only by _root_. This new file also allowed password aging and expiration features to be implemented.

- Like _/etc/passwd_, each user has a line in the _/etc/shadow_ file. A sample line with its nine colon-separated fields is shown below:-

  ```bash
    1                     2                3     4     5     6   7     8      9
  user03 : $6$CSsX...output omitted... : 17933 : 0 : 99999 : 7 : 2 : 18113 :
  ```

  **1** : Username of the account this password belongs to.

  **2** : The encrypted password of the user. The format of encrypted passwords is discussed later

  **3** : The day on which the password was last changed. This is set in days since 1970-01-01, and is calculated in the UTC time zone.

  **4** : The minimum number of days that have to elapse since the last password change before the user can change it again.

  **5** : The maximum number of days that can pass without a password change before the password expires. An empty field means it does not expire based on time since the last change.

  **6** : Warning period. The user will be warned about an expiring password when they login for this number of days before the deadline.

  **7** : Inactivity period. Once the password has expired, it will still be accepted for login for this many days. After this period has elapsed, the account will be locked.

  **8** : The day on which the account expires. This is set in days since 1970-01-01, and is calculated in the UTC time zone. An empty field means it does not expire on a particular date.

  **9** : The last field is usually empty and is reserved for future use.

- **Format of encrypted Password:** The encrypted password field stores three pieces of information: the hashing algorithm used, the salt, and the encrypted hash. Each piece of information is delimited by the _$_ sign

  ```bash
    1           2                        3
  $ 6 $ 2CSsXcYG1L/4ZfHr/ $ 2W6evvJahUfzfHpc9X.45Jc6H30E...
   ```

  **1** : The hashing algorithm used for this password. The number 6 indicates it is a SHA-512 hash, which is the default in Red Hat Enterprise Linux 8. A 1 would indicate MD5, a 5 SHA-256.

  **2** : The salt used to encrypt the password. This is originally chosen at random.

  **3** : The encrypted hash of the user's password. The salt and the unencrypted password are combined and encrypted to generate the encrypted hash of the password.

  The primary reason to combine a salt with the password is to defend against attacks using pre-computed lists of password hashes. Adding salts changes the resulting hashes, making the pre-computed list useless. If an attacker is able to obtain a copy of an /etc/shadow file that is using salts, they will need to perform brute-force password guessing, requiring more time and effort.

- **Password Verification:** When a user tries to log in, the system looks up the entry for the user in /etc/shadow, combines the salt for the user with the unencrypted password that was typed in, and encrypts them using the hashing algorithm specified. If the result matches the encrypted hash, the user typed in the right password. If the result does not match the encrypted hash, the user typed in the wrong password and the login attempt fails. This method allows the system to determine if the user typed in the correct password without storing that password in a form usable for logging in.

- **Configuring Password Aging:**

  - The default password aging policies are set in the _/etc/login.defs_ file. to set the default password aging policies.
    - The PASS_MAX_DAYS sets the default maximum age of the password.
    - The PASS_MIN_DAYS sets the default minimum age of the password.
    - The PASS_WARN_AGE sets the default warning period of the password.

  - You can edit the password aging configuration items in the _/etc/login.defs_ file to change the default password aging policies. however, any change in the default password aging policies will be effective for new users only. The existing users will continue to use the old password aging settings rather than the new ones.

  - Password aging policy for a particular user can also be changed using the **_chage_** command. use `chage --help` command to learn about all the available options. Yo can also checkout this [page](https://www.howtoforge.com/linux-chage-command/) for more exmamples.

### Restricting Access

- There are two ways of Restricting access for an account:-

  - **Lock/Expire an account**
  - **The nologin Shell**

- **Difference between locking and expiring a user account?:-**

  - The locking mechanism works only for local password login. Therefore, Locking the account will only prevent the user from authenticating with a password, not with other login mechanisms like PAM or ssh key. On the other hand, the expiration mechanism is needed to expire the account in the future. Say like a service account that can be used for a week or so.

  - If you want to disable an account, you also have to expire it, not just lock it.

  - If you hire a contractor for 6 months and you want the account to be disabled at the end of the contract, you can set an account expiration at a fixed date and you won't have to be concerned about removing access to this contractor when the contract is finished since the account will be automatically disabled.

  - Expiration does not mean that the user and the files owned by the user will be deleted. Therefore, If the employee returns, the account can later be enabled again.



- **Lock an account:**  you can lock a user's account by running the _usermod_ command along with `-L` or `--lock` option.

     ```bash
     [user01@host ~]$ sudo usermod -L user03
     [user01@host ~]$ su - user03
     Password: redhat
     su: Authentication failure
     ```

  If you want to disable an account, you also have to expire it, not just lock it. You can again use the `usermod` command along with the `-L` option to locks the user's password and also the `-e` option to set the account expiry date. The date must be given as the number of days since 1970-01-01, or in the YYYY-MM-DD format. 

    ```bash
    [user01@host ~]$ sudo usermod -L -e 2021-12-31 user03
    ```

  The above command will immediately lock the user account for the _'user03'_ user and also, the account will expire on 31st December, 2021. The account can later be unlocked with `usermod -U` command. If the account was also expired, be sure to also change the expiration date as well.


- **The noLogin shell:**  The nologin shell acts as a replacement shell for the user accounts not intended to interactively log into the system. It is wise from a security standpoint to disable an account from logging into the system, when the account does not require it. For example, a mail server may require an account to store mail and a password for the user to authenticate with a mail client used to retrieve mail. That user does not need to log directly into the system.

  A common solution to this situation is to set the user's login shell to _/sbin/nologin_. If the user attempts to log in to the system directly, the nologin shell closes the connection.

   ```bash
   [user01@host ~]$ usermod -s /sbin/nologin user03
   [user01@host ~]$ su - user03
   Last login: Wed Feb  6 17:03:06 IST 2019 on pts/0
   This account is currently not available.
   ```

  **Note:** The nologin shell prevents interactive use of the system, but does not prevent all access. Users might be able to authenticate and upload or retrieve files through applications such as web applications, file transfer programs, or mail readers if they use the user's password for authentication.

- You can also refer to the below links for more detailed information:-
  - [Four ways to lock & unlock a user account in Linux](https://www.2daygeek.com/lock-unlock-disable-enable-user-account-linux/)
  - [Locking and unlocking accounts on Linux systems](https://www.networkworld.com/article/3513982/locking-and-unlocking-accounts-on-linux-systems.html)

## **6.12.** Summary

- There are three main types of user account: the superuser, system users, and regular users.
- A user must have a primary group and may be a member of one or more supplementary groups.
- The three critical files containing user and group information are _/etc/passwd_, _/etcgroup_, and _/etc/shadow_.
- The _su_ and _sudo_ commands can be used to run commands as the superuser.
- The _useradd_, _usermod_, and _userdel_ commands can be used to manage users.
- The _groupadd_, _groupmod_, and _groupdel_ commands can be used to manage groups.
- The _chage_ command can be used to configure and view password expiration settings for users.

# **Chapter 7:** Controlling Access to Files

## **7.1.** Interpreting Linux File System Permissions

### Ownership and Permissions of File and Directory in Linux

- For effective security, Linux divides authorization for a file into 2 levels:-
  - **Ownership** (_user_, _group_, _others_)
  - **Permission** (_rwx_)

- Files have three owning user categories to which permissions apply.:-
  - **user**: The file is owned by a user, normally the one who created the file. 
  - **group**: The file is also owned by a single group, usually the primary group of the user who created the file, but this can be changed.
  - **others**: It means everybody else. Hence, when you set the permission for others, it is also referred as set permissions for the world.
  
- Three permission categories apply: _read_, _write_, and _execute_. The following table explains how these permissions affect access to files and directories.

   | Permission | Effect on files | Effect on directories 
   |------------|-----------------|-----------------------
   | r (read) | File contents can be read. | the names of the files in it can be listed, but no other information, including permissions or time stamps, are available, nor can they be accessed. |
   | w (write) | File contents can be changed. | Any file in the directory can be created or deleted. |
   | x (execute) | Files can be executed as commands. | The directory can be navigated i.e. you can **cd** into it, but also require read permission to list files found there. If a directory doesn't have execute permission, you cannot navigate into the directory. Also, If a user only has execute access on a directory, they cannot list file names in the directory. If they know the name of a file that they have permission to read, they can access the contents of that file from outside the directory by explicitly specifying the relative file name.|

- **Note:** A file may be removed by anyone who has:-
  - ownership of the file
  - write permission for the directory in which the file resides, regardless of the ownership or permissions on the file itself. However this can be overridden with a special permission, **the sticky bit**, which is discussed later.

- **An example:** **joshua** is a member of the groups _joshua_ and _web_, and **allison** is a member of _allison_, _wheel_, and _web_. When joshua and allison need to collaborate, the files should be associated with the group _web_ and group permissions should allow the desired access.

### Viewing File and Directory Permissions and Ownership

- The `-l` option of the `ls` command shows detailed information about permissions and ownership:

   ```bash
   [user@host~]$ ls -l test
   -rw-rw-r--. 1 student student 0 Feb  8 17:36 test
   ```

   Use the -d option to show detailed information about a directory itself, and not its contents. 

   ```bash
   [user@host ~]$ ls -ld /home
   drwxr-xr-x. 5 root root 4096 Jan 31 22:00 /home
   ```

- The aboove output is divided into 9 parts. They are:-

   ```bash
        1      2   3       4     5  6   7   8    9
   -rw-rw-r--. 1 student student 0 Feb  8 17:36 test
   ```

  - **1**: type of file and file permissions
  - **2**: number of hard links of the file
  - **3**: _user_ that owns the file
  - **4**: _group_ that owns the
  - **5**: file size in bytes
  - **6**: abbreviated month file was last modified
  - **7**: day-of-month file was last modified
  - **8**: hour and minute file was last modified
  - **9**: Name of the file

- The first character of the long listing is the file type, interpreted like this:-
  - **-** is a regular file.
  - **d** is a directory.
  - **l** is a soft link.
  - Other characters represent hardware devices (**b** and **c**) or other special-purpose files (**p** and **s**).

### Examples of Permission Effects

- The following examples will help illustrate how file permissions interact. For these examples, we have four users with the following group memberships:

  User | Group Memberships
  -----|------------------
  operator1 | operator1, consultant1
  database1 | database1, consultant1
  database2 | database2, operator2
  contractor1 | contractor1, operator2

- This is a long listing of the files in that directory:-

  ```bash
  [database1@host dir]$ ls -la
  total 24
  drwxrwxr-x.  2 database1 consultant1   4096 Apr  4 10:23 .
  drwxr-xr-x. 10 root      root          4096 Apr  1 17:34 ..
  -rw-rw-r--.  1 operator1 operator1     1024 Apr  4 11:02 lfile1
  -rw-r--rw-.  1 operator1 consultant1   3144 Apr  4 11:02 lfile2
  -rw-rw-r--.  1 database1 consultant1  10234 Apr  4 10:14 rfile1
  -rw-r-----.  1 database1 consultant1   2048 Apr  4 10:18 rfile2
  ```

- The following table explores some of the effects of this set of permissions for these users:

  | Effect | Why is this true? |
  |--------|-------------------|
  | The user operator1 can change the contents of rfile1. | User operator1 is a member of the consultant1 group, and that group has both read and write permissions on rfile1.|
  | The user database1 can view and modify the contents of rfile2. | User database1 owns the file and has both read and write access to rfile2. |
  | The user operator1 can view but not modify the contents of rfile2 (without deleting it and recreating it). | User operator1 is a member of the consultant1 group, and that group only has read access to rfile2. |
  | The users database2 and contractor1 do not have any access to the contents of rfile2. | other permissions apply to users database2 and contractor1, and those permissions do not include read or write permission. |
  | operator1 is the only user who can change the contents of lfile1 (without deleting it and recreating it). | User and group operator1 have write permission on the file, other users do not. But the only member of group operator1 is user operator1. |
  | The user database2 can change the contents of lfile2. | User database2 is not the user that owns the file and is not in group consultant1, so other permissions apply. Those grant write permission. |
  | The user database1 can view the contents of lfile2, but cannot modify the contents of lfile2 (without deleting it and recreating it). | User database1 is a member of the group consultant1, and that group only has read permissions on lfile2. Even though other has write permission, the group permissions take precedence. |
  | The user database1 can delete lfile1 and lfile2. | User database1 has write permissions on the directory containing both files (shown by .), and therefore can delete any file in that directory. This is true even if database1 does not have write permission on the file itself. |

## **7.3.** Managing File System Permissions from the Command Line

### Changing File and Directory Permissions

- The command used to change permissions from the command line is chmod, which means "change mode" Permissions are also called the mode of a file.

- The chmod command takes a permission instruction followed by a list of files or directories to change. The permission instruction can be issued in 2 ways:-
  - symbolically (the symbolic method)
  - numerically (the numeric method)

- **Changing Permissions with the Symbolic Method:** 
  - The symbolic method of changing file permissions uses letters to represent the different groups of permissions.

    ```bash
    chmod WhoWhatWhich file|directory
    ```

    - **Who** is _u_, _g_, _o_, _a_ (for user, group, other, all)
    - **What** is _+_, _-_, _=_ (for add, remove, set exactly)
    - **Which** is _r_, _w_, _x_ (for read, write, execute)

  - **Note**:
    - `a` means All users, identical to `ugo`
    - `=` will override all the current permissions to the specified permissions. If no permissions are specified after the `=` symbol, all permissions are removed from the specified _user_, _group_ or _other_. You can also use `=` to assign the user, exact same permission as the specified user. For example, `g=u` will give _other users_ exactly the same permission whatever the _owner_ of the file has.


  - **Symbolic Method Examples:** Below are few use cases for setting different permissions for a file:-
  
    ```bash
    # viewing current permissions for 'sample' file
    [home@virtualbox]$ ls -l sample
    -rw-rw-r-- 1 home home 55 2012-09-10 10:59 sample
  
    # Adding execute permission to the user and group
    [home@virtualbox]$ chmod ug+x sample
    [home@virtualbox]$ ls -l sample
    -rwxrwxr-- 1 home home 55 2012-09-10 10:59 sample
  
    # Removing execute permission from group
    [home@virtualbox]$ chmod g-x sample
    [home@virtualbox]$ ls -l sample
    -rwxrw-r-- 1 home home 55 2012-09-10 10:59 sample
  
    # set only read permission for group
    # using = will override all the existing permissions and set only read permission
    [home@virtualbox]$ chmod g=r sample
    [home@virtualbox]$ ls -l sample
    -rwxr--r-- 1 home home 55 2012-09-10 10:59 sample
  
    # provide 'group' exact same permission that the owner of teh file has
    [home@virtualbox]$ chmod g=u sample
    [home@virtualbox]$ ls -l sample
    -rwxr--rwx 1 home home 55 2012-09-10 10:59 sample
  
    # Provide only read permission to all (user, group, others)
    [home@virtualbox]$ chmod a=r sample
    [home@virtualbox]$ ls -l sample
    -r--r--r-- 1 home home 55 2012-09-10 10:59 sample
  
    # Provide rwx to owner, rw to group and r to other
    [home@virtualbox]$ chmod u=rwx,g=rw,o=r sample
    [home@virtualbox]$ ls -l sample
    -rwxrw-r-- 1 home home 55 2012-09-10 10:59 sample
  
    # You can also give same set of permissions to multiple files at once
    [home@virtualbox]$ chmod u=rwx,g=rw,o=r file1 file2 file3
    ```

- **Changing Permissions with the Numeric Method:-**

  - In this mode, file permissions are not represented as characters but a three or four digit octal number. 4-digit octal number are used when setting advanced permissions.

  - When 3 digits number is used, the first digit represents the permissions of the file’s owner, the second one the file’s group, and the last one all other users. Each write, read, and execute permissions have the following number value:-
    - r (_read_) = 4
    - w (_write_) = 2
    - x (_execute_) = 1
    - no permissions = 0

  - The permissions number of a specific user class is represented by the sum of the values of the permissions for that group. For example:-
    - **rwx** :4+2+1 = 7
    - **r-x** : 4+0+1 = 5
    - **r- -** : 4+0+0 = 4
    - **- - -** : 0+0+0 = 0

  - **Examples:-**

      ```bash
      # Set read and write permissions for user, read permission for group and other, on samplefile
      [user@host ~]$ chmod 644 samplefile

      # Set read, write, and execute permissions for user, read and execute permissions for group, and no permission for other on sampledir
      [user@host ~]$ chmod 750 sampledir

      # You can check the file’s permissions in the numeric notation using the stat command
      [user@host ~]$ stat -c "%a" samplefile
      644
      ```

  - When the 4 digits number is used, the first digit has the following meaning:-
    - _setuid_=4
    - _setgid_=2
    - _sticky_ bit=1
    - _no changes_ = 0

  - So, When the 4 digits number is used, the first digit is used to to set up the `setuid`, `setgid`, and `sticky bit` flags. The next three digits have the same meaning as when using 3 digits number.

  - If the first digit is 0 it can be omitted, and the mode can be represented with 3 digits. The numeric mode `0755` is the same as `755`.

- **Operating on Symbolic Links:** Symbolic links will always have `777` permissions. If you try to change the permissions of a symbolic link, `chmod` will change the permissions of the actual file the link is pointing to. 

  One thing to note is that, you might not be able to change the target file permissions. Instead you might get a “_cannot access ‘symlink’: Permission denied_” error. The error occurs because by default on most Linux distributions symlinks are protected, and you cannot operate on target files.
  
- **Using a Reference File:** The `--reference` option allows you to set the file’s permissions to be same as those of the specified reference file. For example, the following command will assign the permissions of the _file1_ to _file2_:-

  ```bash
  chmod --reference=file1 file2
  ```

- **Changing the permissions of files recursively:** Sometimes you would want to change the permissions of all files and subdirectories present inside a specific directory. The `chmod` command supports the `-R` option to recursively set permissions on the files in an entire directory tree using both symbolic or numeric mode.

  - For example, to change the permissions of all files and subdirectories under the /var/www/html directory to 755 you would use:

    ```bash
    chmod -R 755 /var/www/html
    ```

    The mode can also be specified using the symbolic method:

    ```bash
    chmod -R u=rwx,go=rx /var/www/html
    ```

  - **WARNING:** As you know, _execute_ permission on directories is required for traversal. So you might think of doing something like this:-

    ```bash
    chmod -R u=rwx,g=rx,o=g /var/somedirectory
    ```
  
    This would probably work, but would leave you in a sad state because you'll also make all the files executable, even those that are not supposed to be executable at all. This may be just annoying and may get risky as well. Thus, we have a great alternative. When using the `-R` option, it can be useful to set permissions symbolically using the `X` option.think doing something like this:-

      ```bash
      chmod -R u=rwX,g=rX,o=g /var/somedirectory
      ```

  - Using the uppercase X has the following advantages ove the lowercase x:- 
    - X will provide excute permission for all the sub-directories, so that they can be traversed.
    - when it comes to files, it will provide execute permission only to those files which already had the execute permissions set. This way you avoid the risk of unnecessarily granting the execute permission to the files which are not meant to be executable.
    - Most important benefit is that using the lowercase x, it would be impossible to achieve this result with one command only.

- **Changing File Permissions in Bulk:** Sometimes there are situations where you would need to bulk change files and directories permissions. The most common scenario is to recursively change the website file’s permissions to 644 and directory’s permissions to 755.

  - Using the numeric method:
  
    ```bash
    find /var/www/my_website -type d -exec chmod 755 {} \;
    find /var/www/my_website -type f -exec chmod 644 {} \;
    ```

  - Using the symbolic method:

    ```bash
    find /var/www/my_website -type d -exec chmod u=rwx,go=rx {} \;
    find /var/www/my_website -type f -exec chmod u=rw,go=r {} \;
    ```

  The **find** command will search for files and directories under _/var/www/my_website_ and pass each found file and directory to the chmod command to set the permissions.

### Changing File and Directory User or Group Ownership

- A newly created file is owned by the user who creates that file. By default, new files have a group ownership that is the primary group of the user creating the file.

- In Red Hat Enterprise Linux, a user's primary group is usually a private group with only that user as a member. To grant access to a file based on group membership, the group that owns the file may need to be changed.

- Only _root_ can change the user that owns a file. Group ownership, however, can be set by _root_ or by the file's owner.

- _root_ can grant file ownership to any group. But regular users can make a group as the owner of a file, only if they are a member of that group.

- File ownership can be changed with the chown (**ch**ange **own**er) command.

  ```bash
  # grant ownership of the 'test_file' file to the 'student' user
  [root@host ~] chown student test_file

  # grants ownership of 'test_dir' and all files and subdirectories within it to 'student' user
  [root@host ~] chown -R student test_dir
   
  # you can grant ownership to a group using the ':group' syntax
  # changes the group ownership of the 'test_dir' directory to 'admins' group
  [root@host ~] chown :admins test_dir

  # you can change both owner and group at the same time by using the 'owner:group' syntax
  # to change the ownership of 'test_dir' to 'visitor' user and the 'guests' group
  [root@host ~] chown visitor:guests test_dir
  ```

- **`chown` vs `chgrp`:-**
  - Instead of using `chown`, some users change the group ownership by using the `chgrp` command. This command works just like _chown_, except that it is only used to change group ownership and the colon (:) before the group name is not required.

  - **Important:** You may encounter examples of `chown` commands using an alternative syntax that separates owner and group with a period instead of a colon.

    ```bash
    [root@host ~] chown owner.group filename
    ```

    _You should not use this syntax. Always use a colon,_  because a period is a valid character in a user name, but a colon is not. This can be confusing and may lead to unexpected results.
  
    For example, If there exists users named _enoch.root_ and _enoch_, and also if a group exists with name _root_ on the system, the result of `chown enoch.root filename` will be to have filename owned by the user '_enoch.root_'. You may have been trying to set the file ownership to the _enoch_ user and group _root_.  Therefore, If you always use the _chown_ colon syntax when setting the user and group at the same time, the results are always easy to predict.

## **7.5.** Managing Default Permissions and File Access

### Special Permissions

- Special permissions constitute a fourth permission type in addition to the basic user, group, and other types. As the name implies, these permissions provide additional access-related features over and above what the basic permission types allow. This section details the impact of special permissions, summarized in the table below:-

  | Special permission | Effect on files | Effect on directories |
  |--------------------|-----------------|-----------------------|
  | suid | File executes as the user that owns the file, not the user that ran the file. | No effect.|
  | sgid | File executes as the group that owns the file. | Files newly created in the directory have their group owner set to match the group owner of the directory. |
  | sticky bit | No effect. | Users with write access to the directory can only remove files that they own; they cannot remove or force saves to files owned by other users. |

- Setting Special Permissions:-
  - **Symbolically**: setuid = u+s; setgid = g+s; sticky = o+t
  - **Numerically** (fourth preceding digit): setuid = 4; setgid = 2; sticky = 1 

- **Set-user-ID (SUID):** In Linux by default when a user executes a file, The file gets executed with the privileges of the user who executes it. If we set SUID(set-user-ID) bit on the executable this behavior can be changed, then the file will always run with privileges of the owner of the file, no matter who runs the executable. 

   In other words, the setuid permission on an executable file(say script) means that commands available on the script will run as the user owning the file, not as the user that ran the command. One example is the `passwd` command:

    ```bash
    # As you notice “s” letter instead of usual “x” to execute permission for the owner. This letter “s” indicates that SUID(set-user-ID) bit has been set for the file or directory specified and the file is executable too. If the owner does not have execute permissions, this is replaced by an uppercase S.
    [user@host ~]$ ls -l /usr/bin/passwd
    -rwsr-xr-x. 1 root root 35504 Jul 16  2010 /usr/bin/passwd
    ```

  Only owner of the file or root can set the SUID bit. Below example shows how you can set the SUID bit:-

  ```bash
  # view file permissions
  [home@virtualbox]$ ls -l sample
  -rwxrw-r-- 1 home home 55 2012-09-10 10:59 sample

  # set SUID using symbolic method
  [home@virtualbox]$ chmod u+s sample

  # you can also use octal notations to set SUID by prefixing “4” to the octal string
  [home@virtualbox]$ chmod 4766 sample

  # view file permissions again
  [home@virtualbox]$ ls -l sample
  -rwsrw-r-- 1 home home 55 2012-09-10 10:59 sample

  # As you notice “s” letter instead of usual “x” to execute permission for the owner.

  # remove SUID bit
  [home@virtualbox]$ chmod u-s sample

  # using octal notation
  [home@virtualbox]$ chmod 766 sample
  ```

- **Set-group-ID bit on a file:** 
  - Set-group-ID (SGID) is similar to SUID except that, an executable with SGID bit set runs with the privileges of the group which owns of the file.  In other words, if _setgid_ is set on an executable script file, commands present on the script run as the group that owns that file, not as the user that ran the command, in a similar way to setuid works. One example is the `locate` command:

    ```bash
    [user@host ~]$ ls -ld /usr/bin/locate
    -rwx--s--x. 1 root slocate 47128 Aug 12 17:17 /usr/bin/locate
    ```

  - You can set SGID bit by passing `chmod g+s` command. Alternatively, you can use octal notional by prefixing “2” to the octal string(like 2755 instead of 755).

- **Set-group-ID bit on a directory:** 
  - When set-group-ID (SGID) bit is set for a directory, all newly created subdirectories/files under the directory inherit their group ownership from the directory, rather than inheriting it from the creating user.

  - Set-group-ID is very useful in multi-user. This is commonly used on group collaborations where users with different primary group have access to each others files. Setting SGUID bit on a directory helps creating a shared folder between two local users. This will automatically change the group ownership of newly created files or sub-directories from the default private group to the shared group.

  - An example of this is the _/run/log/journal_ directory:

     ```bash
     [user@host ~]$ ls -ld /run/log/journal
     drwxr-sr-x. 3 root systemd-journal 60 May 18 09:15 /run/log/journal
     ```

- **The Sticky Bit:**
  - the sticky bit for a directory sets a special restriction on deletion of files. This special permission is useful to prevent users from deleting other user’s file inside a shared folder where everyone has read, write, and execute access.

  - If the sticky bit on a directory is set, subdirectories/Files under that directory can only be deleted by either owner of the file, owner of the directory, or the root user. An example is _/tmp_ directory:

     ```bash
     [user@host ~]$ ls -ld /tmp
     drwxrwxrwt. 39 root root 4096 Feb  8 20:52 /tmp
     ```

  - In the long listing above, you can identify the sticky permissions by a lowercase **t** where you would normally expect the **x** (other execute permissions) to be. If other does not have execute permissions, this is replaced by an uppercase **T**.

### Default File Permissions

- When you create a new file or directory, Linux applies a default set of permissions. The `umask` command lets you change these default permissions.

- If you create a new directory, the operating system starts by assigning it octal permissions 0777 (drwxrwxrwx). If you create a new regular file, the operating system assignes it octal permissions 0666 (-rw-rw-rw-).
  
  **Note:** You always have to explicitly add execute permission to a regular file. This makes it harder for an attacker to compromise a network service so that it creates a new file and immediately executes it as a program.

- However, the shell session will also set a umask to further restrict the permissions that are initially set. This is an octal bitmask used to clear the permissions of new files and directories created by a process. This is explained below.

- Linux uses the following default mask and permission values:-
  - The system default permission values are **0777** (_rwxrwxrwx_) for folders and **0666** (_rw-rw-rw-_) for files.

  - The default mask for a non-root user is **0002**, changing the folder permissions to **0775** (_rwxrwxr-x_), and file permissions to **664** (_rw-rw-r--_).

  - The default mask for a root user is **0022**, changing the folder permissions to **0755** (_rwxr-xr-x_), and file permissions to **644** (_rw-r--r--_).

- **How to Calculate Umask Values:** The final permission value is the result of subtracting the umask value form the default permission value (777 or 666). For example, if you want to change the folder permission value from 777 (read, write, and execute for all) to 444 (read for all), you need to apply a umask value of 333, since:

  ```bash
  # Desired Permission = Default Permission - Mask Value
  444 = 777 - Mask Value
  Mask Value = 777 - 444
  Mask value = 333
  ```

- **The umask Command Syntax:**
  - The umask command uses the following syntax:

      ```bash
      umask [-p] [-S] [mask]
      ```

    Where:
    - **[mask]**: The new permissions mask you are applying. By default, the mask is presented as a numeric (octal) value.
    - **[-S]**: Displays the current mask as a symbolic value.
    - **[-p]**: Displays the current mask along with the umask command, allowing it to be copied and pasted as a future input.

  - Here's the example:-

      ```bash
     # umask command without additional command options returns the mask of the current shell
     [user@host ~]$ umask
     0002

     # Displays the current mask as a symbolic value.
     [user@host ~]$ umask -S
     u=rwx,g=rwx,o=rx

     # Displays the current mask along with the umask command
     [user@host ~]$ umask -p
     umask 0002

     # To set/update the Umask value of current shell
     [user@host ~]$ umask 0003
     [user@host ~]$ umask
     0003

     # You can also omit any leading zeros in the umask
     [user@host ~]$ umask 2
     [user@host ~]$ umask
     0002

     # You can also use a symbolic umask value
     [user@host ~]$ umask 0003
     [user@host ~]$ umask
     0002
     ```

  - **Set umask Using Symbolic Values:**
    - You can also use a symbolic value to update/set the umask value of current shell, using the following syntax, where **#** represents the symbolic permission value you want to apply (**Avoid using symbolic values, it's pretty confusing**)

       ```bash
       umask u=#,g=#,o=#
       ```

      - Never use space after comas when setting up a symbolic mask value.
      - There are also other operators you can use:-
        - **=:** Creates specified file permissions and prohibits unspecified permissions.
        - **+:** Creates specified permissions, but does not change unspecified permissions.
        - **-:** Prohibits specified permissions, but does not change unspecified permissions.

    - For Example:-

      ```bash
       #u=rwx (4+2+1=7)
       #g= (0)
       #o= (0)
       #umask value - (0777-0700 = 0077)
       [user@host ~]$ umask u=rwx,g=,o=
       [user@host ~]$ umask
       0077
  
       #u=rwx (4+2+1=7)
       #g=rx (4+1=5)
       #o=rx (4+1=5)
       #umask value - (0777-0755 = 0022)
       [user@host ~]$ umask u=rwx,g=rx,o=rx
       [user@host ~]$ umask
       0022
       ```

- **How to Set or Update the Default Umask Value:**
  - You can change the umask value for the current shell by simply running the `umask [mask-value]` command in the current shell.

  - However, if you want to update the default umask value itself everytime you start a shell you can do it in following ways:-

    - **Approach 1**:  The default umask for users is set by the shell startup scripts. By default, if your account's UID is 200 or more and your username and primary group name are the same, you will be assigned a umask of 002. Otherwise, your umask will be 022.

      As root, you can change this by adding a shell startup script named /etc/profile.d/local-umask.sh that looks something like the output in this example:

         ```bash
         [root@host ~] cat /etc/profile.d/local-umask.sh
         # Overrides default umask configuration
         if [ $UID -gt 199 ] && [ "`id -gn`" = "`id -un`" ]; then
             umask 007
         else
             umask 022
         fi
         ``` 

       The preceding example will set the umask to 007 for users with a UID greater than 199 and with a username and primary group name that match, and to 022 for everyone else. If you just wanted to set the umask for everyone to 022, you could create that file with just the following content:

         ```bash
         # Overrides default umask configuration
         umask 022
         ```

      To ensure that global umask changes take effect you must either source the file (or) log out of the shell and log back in. Until that time the umask configured in the current shell is still in effect.
  
    - **Approach 2**: The system's(all users) default umask values for Bash shell users are defined in the _/etc/profile_ and _/etc/bashrc_ files. Users can override the system defaults in the _.bash_profile_ and _.bashrc_ files in their home directories. 

       ```bash
       # Open the file for editing
       vi /etc/profile (or) vi ~/.bashrc

       # Append/modify following line in the script file to setup a new umask:
       umask 022

       #For changes to take effect, run the following source command or log out and log in
       source /etc/profile/
       ```

- **Difference Between _umask_ and _chmod_:**
  - The _chmod_ command in Linux works in a similar way to the _umask_ command. It too is used to define permissions for files and folders.

  - The difference between _umask_ and _chmod_ is that umask changes the default permissions and thus the permissions for all newly created files and folders, while chmod sets permissions for files and folders that already exist


## **7.8.* Summary

- Files have three categories to which permissions apply. A file is owned by a user, a single group, and other users. The most specific permission applies. User permissions override group permissions and group permissions override other permissions.

- The **_ls_** command with the _**-l**_ option expands the file listing to include both the file permissions and ownership.

- The `chmod` command changes file permissions from the command line. There are two methods to represent permissions, symbolic (letters) and numeric (digits).

- The `chown` command changes file ownership. The **-R** option recursively changes the ownership of a directory tree.

- The `umask` command without arguments displays the current umask value of the shell. Every process on the system has a umask. The default umask values for Bash are defined in the /etc/profile and /etc/bashrc files.

</br></br>

# **Chapter 8:** Monitoring and Managing Linux Processes

## **8.1.** Listing Processes

- A process is a running instance of a launched, executable program. A process consists of:-
  - An address space of allocated memory
  - Security properties including ownership credentials and privileges
  - One or more execution threads of program code
  - Process state

- The environment of a process includes:-
  - Local and global variables
  - A current scheduling context
  - Allocated system resources, such as file descriptors and network ports

- An existing (parent) process duplicates its own address space (_fork_) to create a new (child) process structure. Every new process is assigned a unique process ID (PID) for tracking and security. The PID and the parent's process ID (PPID) are elements of the new process environment.

- Any process may create a child process. All processes are descendants of the first system process, _**systemd**_ on a Red Hat Enterprise Linux 8 system.

- `Control+Z` is used for suspending a process by sending it the signal **_SIGSTOP_**, which cannot be intercepted by the program. While `Control+C` is used to kill a process with the signal _**SIGINT**_, and can be intercepted by a program so it can clean its self up before exiting, or not exit at all.

- **Lifecycle of a process:**
  - Through the _fork routine_, a child process first inherits security identities, previous and current file descriptors, port and resource privileges, environment variables, and program code. Once the inhertitance is complete, the child process then exec its own program code.
  - Normally, a parent process sleeps while the child process runs, setting a request (wait) to be signaled when the child completes. Upon exit, the child process has already closed or discarded its resources and environment. The only remaining resource, called a **_zombie_**, is an entry in the process table.
  - The parent, signalled awake when the child exited, cleans the process table of the child's entry, thus freeing the last resource of the child process. The parent process then continues with its own program code execution.

- In a multitasking operating system, each CPU (or CPU core) can be working on one process at a single point in time. Thus, on a single CPU system, only one process can run at a time. As a process runs, its immediate requirements for CPU time and resource allocation change. Processes are assigned a state, which changes as circumstances dictate.

- **Process States:** Linux process states are described very nicely in a graphical and tabular form in the ROLE course. Please refer the section for more detail. In short, a linux process can be in one of the following states:-
  - **R** -	Running or runnable (on run queue)
  - **D**	- Uninterruptible sleep (waiting for some event)
  - **S**	- Interruptible sleep (waiting for some event or signal)
  - **T**	- Stopped, either by a job control signal or because it is being traced by a debugger.
  - **Z**	- Zombie process, terminated but not yet reaped by its parent.

- On a single CPU system where only one process runs at a time. It is possible to see several processes with a state of **R**. However, that doesn't mean that all of them will be running consecutively, some of them will be in waiting state, which is also reperented using the '**R**' flag.

- Process can be suspended, stopped, resumed, terminated, and interrupted using signals. Signals are discussed in more detail later in this chapter. Signals can be used by other processes or by the kernel itself, or by users logged into the system.

- **Why Process States are Important:**
  - When troubleshooting a system, it is important to understand how the kernel communicates with processes and how processes communicate with each other. At process creation, the system assigns the process a state.
  - The **_S_** column of the _**top**_ command or the _**STAT**_ column of the _**ps**_ command shows the state of each process.

- **Listing Processes:** The **_ps_** command is used for listing current processes. It can provide detailed process information, including:
  - User identification (UID), which determines process privileges
  - Unique process identification (PID)
  - CPU and real time already expended
  - How much memory the process has allocated in various locations
  - The location of process stdout, known as the controlling terminal
  - The current process state

## **8.3.** Controlling Jobs

### Important Prerequisites

- **Terminal vs TTY vs Console vs Shell**
  - **Terminal:** The word Terminal comes from terminate, indicating that it's the terminating end or "terminal" end of a communications process. Hence, Terminal in linux or windows provides endpoints for telnet, ssh, and shells.
  
  - **TTY**: Teletypewriter or “tty” in shorthand was the first kind of physical terminal. Rather than a screen you'd have a literal typewriter in front of you. When you type on it, you're seeing the text on a piece of paper AND inputing that text into a computer. When that computer replies, you'll see the typewriter automatically type on the same paper.

  - **Console:** Folks in the mid 20th century would have a piece of furniture in their living room called a console or console cabinet. A Console in the context of computers is again a physical terminal device with a screen and keyboard combined inside it. But, it's effectively a Terminal.

  - **Shell:** The Terminal isn't smart. It doesn't actually understands and process your inputs. Therefore, it passes the input to the shell to understand and process it. A shell is the program that the terminal sends user input to. The shell then generates output and passes it back to the terminal for display. sh, bash, ksh, powershell, pwsh etc are some examples of Shells.

  In unix terminology, the short answer is:-

  - terminal = an endpoints for users to interact with the computer
  - tty = physical terminal
  - console = physical terminal
  - shell = command line interpreter

  CONCLUSION: In the software world, Terminal or Console or TTY are, for all intents, synonymous. Originally, they meant a piece of equipment through which you could interact with a computer. In the early days of unix, that meant a teletypewriter(tty), or a console. The name “terminal” came from the electronic point of view, and the name “console” from the furniture point of view.

- **Terminal(TTY) vs Pseudo-Terminal (PTY)**
  - The answer is in the name -- "_Pseudo_" meaning "not genuine but having the appearance of".

  - In the olden days, the terminals were physical devices connected to the computer via Universal Asynchronous Receiver and Transmitter(_UART_). There was always a piece of hardware attached with an associated device, be it display hardware or a serial port. Hence, we needed a physical terminal for every input/output device that needs to be connected to a computer. That is why the computers in the olden days were bulky and big.

  - But computers started becoming smaller and smaller, and with telnet and ssh, there came a need for software "Pseudo devices" to do the job of standing in for display hardware. Hence, the terminals became a computer program and it was not a physical device anymore.
  
  - Because of the introduction of "Pseudo devices" Part of  is that "everything now is a file" in the UNIX paradigm. Programs can use file operations (read and/or write) to interact with the devices.
  
  - "Pseudo Terminal" is a software that emulates Terminal hardware, handling input and output in the same way a physical device would so that the software connected is not aware there's not a real device attached. (Check if Pseudo terminal is a Psedo device).

  - So using the word "terminal" in UNIX context today is actually wrong, because everything is a "pseudo-terminal". Thus, when we refer to a Terminal, we're referring to a literal software version of a Terminal. The Windows Terminal or the linux terminal is exactly that.

  - https://dev.to/napicella/linux-terminals-tty-pty-and-shell-192e

- **Pseudo Devices**
  - TBD

- **Process vs Process Group vs Session**
  - **Process:** A process is a running instance of a launched, executable program. Remember that even if you launch a single process, the system still creates a process group.

  - **Process Groups:** Process group is a collection of one or more processes. A process group constitutes of one or more processes sharing the same process group identifier (PGID). A process group has a process group leader, which is the process that creates the group and whose process ID(PID) becomes the process group ID(PGID) of the group.

    **Note**: A process group is a unix kernel concept and Jobs are an internal concept to the shell. In the simple cases, each job in a shell corresponds to a process group in the kernel. Therefore, to keep things simple, think Jobs and process groups as same.

  - **Sessions:** It is a collection of various process groups. All process groups that you launch in your terminal will belong to the same session. Therefore, each terminal can be thought as a session, and can have a foreground process and any number of independent background processes. A job is part of exactly one session: the one belonging to its controlling terminal.

  In Short, processes are grouped together into process groups. Process groups are grouped together into sessions.

- **Controlling Terminal (ctty)**
  - Every session is tied to a terminal from which processes in the session get their input and to which they send their output. Although, that terminal doesn't necessarily become the controlling terminal of the process.
  
  - The controlling terminal is the login session in which a program was invoked. If you log in to a system to start a bash session (or csh, or ksh, or whatever your shell is), then the shell's controlling terminal is your login session. If you then type 'cat /etc/passwd', the controlling terminal of 'cat' is your login session.

  - A terminal can be the controlling terminal for only one session at a time. Although the controlling terminal for a session can be changed, this is usually done only by processes that manage a user's initial logging in to a system.

  - A session may or may not have a controlling terminal (ctty).  don't really have a controlling terminal because Some processes are started by **_init_** or some other mechanism that doesn't require a terminal - Apache, MySQL, Postfix, etc. don't normally have a controlling terminal per se.

  - The ctty controls processes by sending signals to them, hence the name. A process will never receive a signal from a terminal that is not its ctty, although it may receive a signal from a process that is running with a different ctty.

  - With controlling terminal, process is able to tell kernel which process group is foreground process group (in same session). If there is a foreground process group for a terminal, we can control the foreground process group via the terminal, e.g., Ctrl-C/Ctrl-\ to terminate the foreground process group. (A terminal may have only one foreground process group, or may not have any. To put it precisely, a terminal can only be associated with one process session.)

- **Background vs Foreground Job**
  - Most commands issued from an interactive shell run in foreground. That basically means that you must wait for the executed command (or processes) to stop before doing something else. if you have run a command that takes a lot of time to complete, you must wait until it is finished to run another command.

  - If you know before you type a command that it's going to take a really long time to complete, and you want to get something else done in the mean time, you can background it when you start it by putting an ampersand **&** at the end of a command. You can also use ctrl-Z to suspend a foreground process/job and throw it in the background with the `bg` command. You can thereafter manage these backgrounds tasks using `jobs` command.

  - There may be some cases when a background command waits for user input. Thus you will need to bring back that job to foreground. Background processes of a terminal cannot read input or receive keyboard generated interrupts(ctl+c, ctrl+z) from the terminal, but may be able to write to the terminal. A job in the background may be stopped (suspended) or it may be running. If a running background job tries to read from the terminal, it will be automatically suspended.
  
  - If you end your terminal session (through closing the terminal, logout, shutdown, etc.), background jobs that are still running or suspended may be also killed.

  - You can have only one foreground process group in the session. Thus, if you want to run several process groups at the same time then you need background process groups.It is also possible to move the jobs from the background to the foreground and vice-versa using _fg_ or _bg_ command

  - To stop the current running process, you need to enter `CTRL+Z`. This gives you a job number. If needed, the job can be resumed either in the foreground using the `fg command` or the background using the `bg command`. However, By using _fg_ or _bg_ command, it would run only the last stopped process. What if you want to start other than the last stopped process? Just use the job number after fg or bg (say bg %2 or bg %3, etc). If the running job is in the background, you can run any other tasks in the foreground. To get the list of jobs, use command, `jobs`.

  - It is also possible to terminate the process either with CTRL+C or kill command. You can pass the job number while using the kill command.

### Describing Jobs and Sessions

- **_Job control_** is a feature of the shell which allows a single shell instance to run and manage multiple commands. This permits a shell user to simultaneously execute multiple commands (or jobs), one in the foreground and all remaining in the background.

- A job is associated with each pipeline entered at a shell prompt. All processes in that pipeline are part of the job and are members of the same process group. If only one command is entered at a shell prompt, that can be considered to be a minimal “pipeline” of one command, creating a job with only one member.

- Only one job can read input and keyboard generated signals from a particular terminal window at a time. Processes that are part of that job are foreground processes of that controlling terminal.

- A background process of that controlling terminal is a member of any other job associated with that terminal. Background processes of a terminal cannot read input or receive keyboard generated interrupts from the terminal, but may be able to write to the terminal. A job in the background may be stopped (suspended) or it may be running. If a running background job tries to read from the terminal, it will be automatically suspended.

- Each terminal is its own session, and can have a foreground process and any number of independent background processes. A job is part of exactly one session: the one belonging to its controlling terminal.

- The `ps` command shows the device name of the _controlling terminal_ of a process in the TTY column. Some processes, such as _system daemons_, are started by the system and not from a shell prompt. These processes do not have a controlling terminal, are not members of a job, and cannot be brought to the foreground. The **ps** command displays a question mark (?) in the TTY column for these processes.

### **Running Jobs in the Background**

- Any command or pipeline can be started in the background by appending an ampersand (&) to the end of the command line. The Bash shell displays a job number (unique to the session) and the PID(unique system-wide) of the new child process. The shell does not wait for the child process to terminate, but rather displays the shell prompt.

   ```bash
   # Job Number is 1
   # PID 5947
   [user@host ~]$ sleep 10000 &
   [1] 5947
   ```

- When a command line containing a pipe is sent to the background using an ampersand, the PID of the last command in the pipeline is used as output. All processes in the pipeline are still members of that job.

   ```bash
   [user@host ~]$  example_command | sort | mail -s "Sort output" &
   [1] 5998

   # You can display the list of jobs that Bash is tracking for a particular session with the jobs command.
   [user@host ~]$ jobs
   [1]+  Running        sleep 10000 &

   # A background job can be brought to the foreground by using the fg command with its job ID (%job number).
   # the sleep command will then run in the foreground on the controlling terminal. The shell itself is again asleep, waiting for this child process to exit.
   [user@host ~]$ fg %1
   sleep 10000

   # To send a foreground process to the background, first press the keyboard generated suspend request (Ctrl+z) in the terminal. The job is immediately placed in the background and is suspended.
   ^Z
   [1]+  Stopped                 sleep 10000

   # To start the suspended process running in the background, use the bg command with the same job ID.
   [user@host ~]$ bg %1
   [1]+ sleep 10000 &

   # You cannot suspend(ctrl+z) or terminate(ctrl+c) a background process.
   # You can only suspend or terminate a foreground process
   # hence, to terminate or suspend a background process, first bring it to the foreground usinf the fg command and then terminate or suspend it
   [student@servera ~]$ fg %1
   sleep 100000
   ^Z
   [1]+  Stopped                 sleep 10000
   ```

   Note: the `+` sign after the `[1]` in the examples above. The + sign indicates that this job is the current default job. That is, if a command is used that expects a %job number argument and a job number is not provided, then the action is taken on the job with the + indicator.

- The shell will warn a user who attempts to exit a terminal window (session) with suspended jobs. If the user tries exiting again immediately, the suspended jobs are killed.

- The `ps j` command displays information relating to jobs. The _PID_ is the unique process ID of the process. THe _PPID_ is the PID of the parent process of this process, the process that started (forked) it. The _PGID_ is the PID of the process group leader, normally the first process in the job's pipeline. The _SID_ is the PID of the session leader, which (for a job) is normally the interactive shell that is running on its controlling terminal. Since the example sleep command is currently suspended, its process state is T.

  ```bash
  [user@host ~]$ ps j
   PPID   PID  PGID   SID TTY      TPGID STAT   UID   TIME COMMAND
   2764  2768  2768  2768 pts/0     6377 Ss    1000   0:00 /bin/bash
   2768  5947  5947  2768 pts/0     6377 T     1000   0:00 sleep 10000
   2768  6377  6377  2768 pts/0     6377 R+    1000   0:00 ps j
   ```

## **8.5.** Killing Processes

### Process control using signals

- A signal is a software interrupt delivered to a process. Signals report events to an executing program. Events that generate a signal can be an error, external event (an I/O request or an expired timer), or by explicit use of a signal-sending command or keyboard sequence.

- The following table lists the fundamental signals used by system administrators for routine process management. Refer to signals by either their short (HUP) or proper (SIGHUP) name. (In proper name, just add the Prefix ''SIG' to the short name. ex, Short name 'INT', proper name 'SIGINT')

  Signal number | Short name | Definition | Purpose
  --------------|------------|------------|--------
  1 | HUP | Hangup | Used to report termination of the controlling process of a terminal. Also used to request process reinitialization (configuration reload) without termination.
  2 | INT | Keyboard interrupt | Causes program termination. Can be blocked or handled. Sent by pressing INTR key sequence (Ctrl+c).
  3 | QUIT | Keyboard quit | Similar to SIGINT; adds a process dump at termination. Sent by pressing QUIT key sequence (Ctrl+\).
  9 | KILL | Kill, unblockable | Causes abrupt program termination. Cannot be blocked, ignored, or handled; always fatal.
  15 (default) | TERM | Terminate | Causes program termination. Unlike SIGKILL, can be blocked, ignored, or handled. The “polite” way to ask a program to terminate; allows self-cleanup.
  18 | CONT | Continue | Sent to a process to resume, if stopped. Cannot be blocked. Even if handled, always resumes the process.
  19 | STOP | Stop, unblockable | Suspends the process. Cannot be blocked or handled.
  20 | TSTP | Keyboard stop | Unlike SIGSTOP, can be blocked, ignored, or handled. Sent by pressing SUSP key sequence (Ctrl+z).

  NOTE: Signal numbers vary on different Linux hardware platforms, but signal names and meanings are standardized. For command use, it is advised to use signal names instead of numbers. The numbers discussed in this section are for x86_64 systems.

- Each signal has a default action, usually one of the following:
  - **Term** - Cause a program to terminate (exit) at once.
  - **Core** - Cause a program to save a memory image (core dump), then terminate.
  - **Stop** - Cause a program to stop executing (suspend) and wait to continue (resume).

  Programs can be prepared to react to expected event signals by implementing handler routines to ignore, replace, or extend a signal's default action.

- You signal the current foreground process by pressing a keyboard control sequence to suspend (_Ctrl+z_), kill (_Ctrl+c_), or core dump (_Ctrl+\\_) the process. However, you will use **the signal-sending commands** like `kill` to send signals to a background process or to processes in a different session.

- Signals can be specified as options either by name (for example, -HUP or -SIGHUP) or by number (-1).
  
- Users may kill their own processes, but root privilege is required to kill processes owned by others.

- The `kill` command sends a signal to a process by PID number. Despite its name, the kill command can be used to send any signal, not just those for terminating programs. You can use the `kill -l` command to list the names and numbers of all available signals.

   ```bash
   [user@host ~]$ kill -l
   1) SIGHUP      2) SIGINT      3) SIGQUIT     4) SIGILL      5) SIGTRAP
   6) SIGABRT     7) SIGBUS      8) SIGFPE      9) SIGKILL    10) SIGUSR1
  11) SIGSEGV    12) SIGUSR2    13) SIGPIPE    14) SIGALRM    15) SIGTERM
  16) SIGSTKFLT  17) SIGCHLD    18) SIGCONT    19) SIGSTOP    20) SIGTSTP
  ...output omitted...

  [user@host ~]$ ps aux | grep job
  5194  0.0  0.1 222448  2980 pts/1    S    16:39   0:00 /bin/bash /home/user/bin/  control job1
  5199  0.0  0.1 222448  3132 pts/1    S    16:39   0:00 /bin/bash /home/user/bin/  control job2
  5205  0.0  0.1 222448  3124 pts/1    S    16:39   0:00 /bin/bash /home/user/bin/  control job3
  5430  0.0  0.0 221860  1096 pts/1    S+   16:41   0:00 grep --color=auto job

  [user@host ~]$ kill 5194

  [user@host ~]$ ps aux | grep job
  user   5199  0.0  0.1 222448  3132 pts/1    S    16:39   0:00 /bin/bash /home/user/bin/control job2
  user   5205  0.0  0.1 222448  3124 pts/1    S    16:39   0:00 /bin/bash /home/user/bin/control job3
  user   5783  0.0  0.0 221860   964 pts/1    S+   16:43   0:00 grep --color=auto job
  [1]   Terminated              control job1

  [user@host ~]$ kill -9 5199
  [user@host ~]$ ps aux | grep job
  user   5205  0.0  0.1 222448  3124 pts/1    S    16:39   0:00 /bin/bash /home/user/bin/control job3
  user   5930  0.0  0.0 221860  1048 pts/1    S+   16:44   0:00 grep --color=auto job
  [2]-  Killed                  control job2

  [user@host ~]$ kill -SIGTERM 5205
  user   5986  0.0  0.0 221860  1048 pts/1    S+   16:45   0:00 grep --color=auto job
  [3]+  Terminated              control job3
  ```

- The `killall` command can signal multiple processes, based on their command name.

   ```bash
   [user@host ~]$ ps aux | grep job
  5194  0.0  0.1 222448  2980 pts/1    S    16:39   0:00 /bin/bash /home/user/bin/control job1
  5199  0.0  0.1 222448  3132 pts/1    S    16:39   0:00 /bin/bash /home/user/bin/control job2
  5205  0.0  0.1 222448  3124 pts/1    S    16:39   0:00 /bin/bash /home/user/bin/control job3
  5430  0.0  0.0 221860  1096 pts/1    S+   16:41   0:00 grep --color=auto job

  [user@host ~]$ killall control
  [1]   Terminated              control job1
  [2]-  Terminated              control job2
  [3]+  Terminated              control job3
   ```

- Use `pkill` to send a signal to one or more processes which match selection criteria. Selection criteria can be a command name, a process owned by a specific user, or all system-wide processes. The _pkill_ command includes advanced selection criteria:

  - **Command** - Processes with a pattern-matched command name.
  - **UID** - Processes owned by a Linux user account, effective or real.
  - **GID** - Processes owned by a Linux group account, effective or real.
  - **Parent** - Child processes of a specific parent process.
  - **Terminal** - Processes running on a specific controlling terminal.

   ```bash
   [user@host ~]$ ps aux | grep pkill
  user   5992  0.0  0.1 222448  3040 pts/1    S    16:59   0:00 /bin/bash /home/user/bin/control pkill1
  user   5996  0.0  0.1 222448  3048 pts/1    S    16:59   0:00 /bin/bash /home/user/bin/control pkill2
  user   6004  0.0  0.1 222448  3048 pts/1    S    16:59   0:00 /bin/bash /home/user/bin/control pkill3

  [user@host ~]$ pkill control
  [1]   Terminated              control pkill1
  [2]-  Terminated              control pkill2

  [user@host ~]$ ps aux | grep pkill
  user   6219  0.0  0.0 221860  1052 pts/1    S+   17:00   0:00 grep --color=auto pkill
  [3]+  Terminated              control pkill3

  [user@host ~]$ ps aux | grep test
  user   6281  0.0  0.1 222448  3012 pts/1    S    17:04   0:00 /bin/bash /home/user/bin/control test1
  user   6285  0.0  0.1 222448  3128 pts/1    S    17:04   0:00 /bin/bash /home/user/bin/control test2
  user   6292  0.0  0.1 222448  3064 pts/1    S    17:04   0:00 /bin/bash /home/user/bin/control test3
  user   6318  0.0  0.0 221860  1080 pts/1    S+   17:04   0:00 grep --color=auto test

  [user@host ~]$ pkill -U user

  [user@host ~]$ ps aux | grep test
  user   6870  0.0  0.0 221860  1048 pts/0    S+   17:07   0:00 grep --color=auto test
   ```

### Logging Users Out Administratively

- You may need to log other users off for any of a variety of reasons. To name a few of the many possibilities:
  - the user committed a security violation
  - the user may have overused resources
  - the user may have an unresponsive system
  - the user has improper access to materials. 
  
  In these cases, you may need to administratively terminate their session using signals.

- To log off a user, first identify the login session to be terminated. Use the `w` command to list user logins and current running processes. Note the _TTY_ and _FROM_ columns to determine the sessions to close.

   ```bash
   [user@host ~]$ w
   12:43:06 up 27 min,  5 users,  load average: 0.03, 0.17, 0.66
   USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU   WHAT
   root     tty2                      12:26   14:58   0.04s  0.04s  -bash
   bob      tty3                      12:28   14:42   0.02s  0.02s  -bash
   user     pts/1    desk.example.com 12:41    2.00s  0.03s  0.03s   w
   ```

  - All user login sessions are associated with a terminal device (TTY). If the device name is of the form **_pts/N_**, it is a _pseudo-terminal_ associated with a graphical terminal window or remote login session. If it is of the form **_ttyN_**, the user is on a system console, alternate console, or other directly connected terminal device.

  - Discover how long a user has been on the system by viewing the session login time. For each session, CPU resources consumed by current jobs, including background tasks and child processes, are in the _JCPU column_. Current foreground process CPU consumption is in the _PCPU column_.

- Processes and sessions can be individually or collectively signaled. To terminate all processes for one user, use the `pkill` command. Because the initial process in a login session (session leader) is designed to handle session termination requests and ignore unintended keyboard signals, killing all of a user's processes and login shells requires using the SIGKILL signal.

  **IMPORTANT:** SIGKILL is commonly used too quickly by administrators. Since the SIGKILL signal cannot be handled or ignored, it is always fatal. However, it forces termination without allowing the killed process to run self-cleanup routines. It is recommended to send SIGTERM first, then try SIGINT, and only if both fail retry with SIGKILL.

- First identify the PID numbers to be killed using `pgrep` command, which operates much like the `pkill` command, including the same options, except that pgrep lists processes rather than killing them.

   ```bash
   [root@host ~]$ pgrep -l -u bob
   6964 bash
   6998 sleep
   6999 sleep
   7000 sleep

   [root@host ~]$ pkill -SIGKILL -u bob
   [root@host ~]$ pgrep -l -u bob
   [root@host ~]$
   ```

- When processes requiring attention are in the same login session, it may not be necessary to kill all of a user's processes. Determine the controlling terminal for the session using the `w` command, then kill only processes referencing the same terminal ID. Unless SIGKILL is specified, the session leader (here, the Bash login shell) successfully handles and survives the termination request, but all other session processes are terminated.

   ```bash
   [root@host ~]$ pgrep -l -u bob
   7391 bash
   7426 sleep
   7427 sleep
   7428 sleep

   [root@host ~]$ w -h -u bob
   bob      tty3      18:37    5:04   0.03s  0.03s -bash

   [root@host ~]$ pkill -t tty3
   [root@host ~]$ pgrep -l -u bob
   7391 bash

   [root@host ~]$ pkill -SIGKILL -t tty3
   [root@host ~]$ pgrep -l -u bob
   [root@host ~]$
   ```

- The same selective process termination can be applied using parent and child process relationships. Use the `pstree` command to view a process tree for the system or a single user. Use the parent process's PID to kill all children they have created. This time, the parent Bash login shell survives because the signal is directed only at its child processes.

   ```bash
   [root@host ~]$ pstree -p bob
   bash(8391)─┬─sleep(8425)
              ├─sleep(8426)
              └─sleep(8427)

   [root@host ~]$ pkill -P 8391
   [root@host ~]$ pgrep -l -u bob
   bash(8391)

   [root@host ~]$ pkill -SIGKILL -P 8391
   [root@host ~]$ pgrep -l -u bob
   bash(8391)
   ```


</br></br>
