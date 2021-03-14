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

## **2.1.** Accessing the Command Line

- A command line is a text-based interface which can be used to input instructions to a computer system. **The Linux command line is provided by a program called the shell**. The shell is basically a program that interprets commands typed in by the user.
  
- Various options for the shell program have been developed over the years, and different users can be configured to use different shells. Most users, however, stick with the current default.

- The default shell for users in Red Hat Enterprise Linux is the GNU Bourne-Again Shell (bash). Bash is an improved version of one of the most successful shells used on UNIX-like systems, the Bourne Shell (sh).

- Using bash to execute commands can be powerful. **The bash shell provides a scripting language that can support automation of tasks**The shell has additional capabilities that can simplify or make possible operations that are hard to accomplish efficiently with graphical tools. 

- When a shell is used interactively, it displays a string when it is waiting for a command from the user. this is called the shell prompt. When a regular user starts a shell, the default prompt ends with a **$** characterThe $ character is replaced by a **#** character if the shell is running as the superuser, root. this makes it more obvious that it is a superuser shell, which helps to avoid accidents and mistakes which can affect the whole system.

- To get a shell prompt you must start a terminal program in the graphical environmentThe shell prompt is provided in an application window of your graphical terminal program.

- In Linux, the most common way to get a shell prompt on a remote system is to use Secure Shell (SSH). Most Linux systems (including Red Hat Enterprise Linux) and macOS provide the OpenSSH command-line program ssh for this purpose.
  
- The ssh command encrypts the connection to secure the communication against eavesdropping or hijacking of the passwords and content.

  Some systems (such as new cloud instances) do not allow users to use a password to log in with ssh for tighter security. An alternative way to authenticate to a remote machine without entering a password is through public key authentication.

  With this authentication method, users have a special identity file containing a private key, which is equivalent to a password, and which they keep secret. their account on the server is configured with a matching public key, which does not have to be secret. When logging in, users can configure ssh to provide the private key and if their matching public key is installed in that account on that remote server, it will log them in without asking for a password.

- Many system administrators choose not to run a graphical environment on their servers. this allows resources which would be used by the graphical environment to be used by the server's services instead.

- A headless server does not have a keyboard and display permanently connected to it. A data center may be filled with many racks of headless servers, and not providing each with a keyboard and display saves space and expense. To allow administrators to log in, a headless server might have a login prompt provided by its serial console, running on a serial port which is connected to a networked console server for remote access to the serial console.

- The first time you log in to a new machine, you will be prompted with a warning from ssh that it cannot establish the authenticity of the host:

  ```bash
  [user@host ~]$ ssh -i mylab.pem remoteuser@remotehost
  the authenticity of host remotehost (192.0.2.42) cannot be established.
  ECDSA key fingerprint is 47:bf:82:cd:fa:68:06:ee:d8:83:03:1a:bb:29:14:a3.
  Are you sure you want to continue connecting (yes/no)? yes
  ```

   Each time you connect to a remote host with ssh, the remote host sends ssh  its host key to authenticate itself and to help set up encrypted  communicationThe ssh command compares that against a list of saved host  keys to make sure it has not changed. If the host key has changed, this  might indicate that someone is trying to pretend to be that host to hijack  the connection which is also known as man-in-the-middle attack. In SSH, host  keys protect against man-in-the-middle attacks, these host keys are unique  for each server, and they need to be changed periodically and whenever a  compromise is suspected.

  You will get this warning if your local machine does not have a host key saved for the remote host. If you enter yes, the host key that the remote host sent will be accepted and saved for future reference. Login will continue, and you should not see this message again when connecting to this host. If you enter no, the host key will be rejected and the connection closed.

  If the local machine does have a host key saved and it does not match the one actually sent by the remote host, the connection will automatically be closed with a warning.

## **2.3.** Accessing the Command Line Using the Desktop

- The desktop environment is the graphical user interface on a Linux system. **The default desktop environment in Red Hat Enterprise Linux 8 is provided by GNOME 3**. It provides an integrated desktop for users and a unified development platform on top of a graphical framework provided by either Wayland (by default) or the legacy X Window System.

- GNOME Shell provides the core user interface functions for the GNOME desktop environmentThe GNOME Shell application is highly customizable. Red Hat Enterprise Linux 8 defaults GNOME Shell's look and feel to the "Standard" theme, which is used in this section. Red Hat Enterprise Linux 7 defaulted to an alternative theme named "Classic" that was closer to the look and feel of older versions of GNOME. Either theme can be selected persistently at login by clicking the gear icon next to the Sign In button that is available after selecting your account but before entering your password. 

- You can view and edit the GNOME keyboard shortcuts used by your account. Open the system menu on the right side of the top bar. Click the Settings button on the bottom of the menu on the left. In the application window that opens, select Devices → Keyboard from the left paneThe right pane will display your current shortcut settings.

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

- The **_/_** directory is the root directory at the top of the file-system hierarchy. Subdirectories of / are used for standardized purposes to organize files by type and purpose. this makes it easier to find files. For example, in the root directory, the subdirectory /boot is used for storing files needed to boot the system.

- The following terms help to describe file-system directory contents:-
  - **static content** remains unchanged until explicitly edited or reconfigured.
  - **dynamic** or **variable** content may be modified or appended by active processes.
  - **persistent content** remains after a reboot, like configuration settings.
  - **runtime content** is process- or system-specific content that is deleted by a reboot.

- The following table lists some of the most important directories on the system by name and purpose:-

  Location | Purpose
  ---------|--------
  /usr  | Installed software, shared libraries, include files, and read-only program data. Important subdirectories include:-<ul><li>**/usr/bin**: User commands.</li><li>**/usr/sbin**: System administration commands</li><li>**/usr/local**: Locally customized software. </li></ul>
  /etc  | Configuration files specific to this system.
  /var  | Variable data specific to this system that should persist between boots. Files that dynamically change, such as databases, cache directories, log files, printer-spooled documents, and website content may be found under /var.
  /run  | Runtime data for processes started since the last boot. this includes process ID files and lock files, among other thingsThe contents of this directory are recreated on reboot. this directory consolidates /var/run and /var/lock from earlier versions of Red Hat Enterprise Linux.
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

  In earlier versions of Red Hat Enterprise Linux, these were distinct directories containing different sets of files.

  In Red Hat Enterprise Linux 7 and later, the directories in / are symbolic links to the matching directories in /usr.

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
  - Every file starts with a single hard link, from its initial name to the data on the file system. When you create a new hard link to a file, you create another name that points to that same dataThe new hard link acts exactly like the original file name. Once created, you cannot tell the difference between the new hard link and the original name of the file.

  - All hard links that reference the same file will have the same link count, access permissions, user and group ownerships, time stamps, and file content. If any of that information is changed using one hard link, all other hard links pointing to the same file will show the new information as well. this is because each hard link points to the same data on the storage device.

  - Even if the original file gets deleted, the contents of the file are still available as long as at least one hard link exists. Data is only deleted from storage when the last hard link is deleted.

  - Hard links have some limitations. Firstly, hard links can only be used with regular files. You cannot use ln to create a hard link to a directory or special file.

  - Secondly, hard links can only be used if both files are on the same file systemThe file-system hierarchy can be made up of multiple storage devices. Depending on the configuration of your system, when you change into a new directory, that directory and its contents may be stored on a different file system. You can use the **df** command to list the directories that are on different file systems.

- **Soft Links or Symbolic Links:-**
  - The ln -s command creates a soft link, which is also called a "symbolic link." A soft link is not a regular file, but a special type of file that points to an existing file or directory.

  - Soft links have some advantages over hard links:-
    - they can link two files on different file systems.
    - they can point to a directory or special file, not just a regular file

  - When the original regular file gets deleted, the soft link will still point to the file but the target is gone. A soft link pointing to a missing file is called a "dangling soft link."

  - One side-effect of the dangling soft link is that if you later create a new file with the same name as the deleted file, the soft link will no longer be "dangling" and will point to the new file.

    Hard links do not work like this. If you delete a hard link and then use normal tools (rather than ln) to create a new file with the same name, the new file will not be linked to the old file.

  - One way to compare hard links and soft links that might help you understand how they work:-
    - A hard link points a name to data on a storage device
    - A soft link points a name to another name, that points to data on a storage device

## **3.9.** Matching File Names with Shell Expansions

- The Bash shell has multiple ways of expanding a command line including pattern matching, home directory expansion, string expansion, and variable substitution. Perhaps the most powerful of these is the path name-matching capability, historically called globbingThe Bash globbing feature, sometimes called “wildcards”, makes managing large numbers of files easier.

- **Pattern Matching:** Globbing is a shell command-parsing operation that expands a wildcard pattern into a list of matching path names. Command-line metacharacters are replaced by the match list prior to command execution. Patterns that do not return matches display the original pattern request as literal textThe following are common metacharacters and pattern classes. 

  Pattern | Matches
  --------|--------
  *  | Any string of zero or more characters.
  ?  | Any single character.
  [abc...]  | Any one character in the enclosed class (between the square   brackets).
  [!abc...]  | Any one character not in the enclosed class.
  [^abc...]  | Any one character not in the enclosed class.
  [[:alpha:]]  | Any alphabetic character.
  [[:lower:]]  | Any lowercase character.
  [[:upper:]]  | Any uppercase character.
  [[:alnum:]]  | Any alphabetic character or digit.
  [[:punct:]]  | Any printable character not a space or alphanumeric.
  [[:digit:]]  | Any single digit from 0 to 9.
  [[:space:]]  | Any single white space character. this may include tabs, newlines, carriage returns, form feeds, or spaces.

- **Tilde Expansion:-** 
  - The Bash shell provides some variables that are prefixed with **‘~’** character which is called Tilde Expansions. Tilde expansion is the process of converting these abbreviations to the directory names that they stand for.

  - Tilde(~) expands to the value of **$HOME** variable. If $HOME is not defined, then it expands to the value of the home directory set for the current user defined in **/etc/passwd** fileThe _/etc/passwd_ file contains the username, real name, identification information, and basic account information for each user.

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

- **Brace Expansion:** Brace expansion is used to generate discretionary strings of characters. Braces contain a comma-separated list of strings, or a sequence expressionThe result includes the text preceding or following the brace definition. Brace expansions may be nested, one inside another. Also double-dot syntax (..) expands to a sequence such that {m..p} will expand to m n o p.

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

  An older form of command substitution uses backticks: `command`. Disadvantages to the backticks form include: 
  - You can visually confuse backticks with single quote marks
  - It has a more complicated and intrusive quoting mechanism


  ```bash
  [user@host glob]$ echo the time is $(date +%M) minutes past $(date +%l%p).
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

  - The backslash (\) is an escape character in the Bash shell. It will protect the character immediately following it from expansion. In the below example, protecting the dollar sign from expansion caused Bash to treat it as a regular character and it did not perform variable expansion on $HOME.

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
  0 | sthin | Standard input | Keyboard | read only
  1 | sthout | Standard output | Terminal | write only
  2 | stherr | Standard error | Terminal | write only
  3+ | filename | Other files | none | read and/or write


### Redirecting Standard Output and Standard Error to a File

- I/O redirection changes how the process gets its input or output. Instead of getting input from the keyboard, or sending output and errors to the terminal, the process reads from or writes to files. Redirection lets you save messages to a file that are normally sent to the terminal window. Alternatively, you can use redirection to discard output or errors, so they are not displayed on the terminal or saved.

- Redirecting sthout suppresses process output from appearing on the terminal. One thing to keep in mind is that redirecting only sthout does not suppress stherr error messages from displaying on the terminal. If you want to discard messages, the special file _/dev/null_ quietly discards channel output redirected to it and is always an empty file.

- If the file storing the output does not exist, it will be created. If the file does exist and the redirection is not the one that appends to the file(> filename), the file's contents will be overwritten. use redirection '>> filename' to append the output to the file.

- Output Redirection Operators:-
    
    <table>
        <tr>
                     <th> Redirection </ th> 
                     <th> Explanation </ th> 
       </tr>
        <tr>
                     <th> > file </ th> 
                     <th> redirect sthout to overwrite a file </ th> 
       </tr>
        <tr>
                     <th> >> file </ th> 
                     <th> redirect sthout to append to a file </ th> 
       </tr>
        <tr>
                     <th> 2> file </ th> 
                     <th> redirect stherr to overwrite a file </ th> 
       </tr>
        <tr>
                     <th> 2> /dev/null </ th> 
                     <th> discard stherr error messages by redirecting to /dev/null </ th> 
       </tr>
        <tr>
                     <th> > file  2>&1 </ th> 
                     <th rowspan = "2"> redirect sthout and stherr to overwrite the same file </ th> 
       </tr>
        <tr>
                     <th> &> file </ th> 
       </tr>
        <tr>
                     <th> >> file  2>&1 </ th> 
                     <th rowspan = "2"> redirect sthout and stherr to append to the same file </ th> 
       </tr>
        <tr>
                     <th> &>> file </ th> 
       </tr>
    </table>

- The order of redirection operations is important. The following sequence redirects standard output to file and then redirects standard error to the same place as standard output (file).

  ```bash
   > file 2>&1
  ``` 

  However, the next sequence does redirection in the opposite order. This redirects standard error to the default place for standard output (the terminal window, so no change) and then redirects only standard output to file.

  ```bash
  2>&1 > file
  ``` 

  Because of this, some people prefer to use the merging redirection operators:-
  - `&>file`	instead of	`>file 2>&1`
  - `&>>file`	instead of	`>>file 2>&1` (in Bash 4 / RHEL 6 and later)

  However, other system administrators and programmers who also use other shells related to bash (known as Bourne-compatible shells) for scripting commands think that the newer merging redirection operators should be avoided, because they are not standardized or implemented in all of those shells and have other limitations.

### Pipelines, Redirection and the 'tee' Command

- A pipeline is a sequence of one or more commands separated by the pipe character (|). A pipe connects the standard output of the first command to the standard input of the next command. 
  
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

Remember if open a new terminal you won't be able to access either of the variables because you are changing that instance. For that you should add your variables in either .profile or .bashrc (if you are using bash).

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