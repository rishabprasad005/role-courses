# Notes

- Use the **cd** command to change your shell's current working directory. If you do not specify any arguments to the command, it will change to your home directory.

- The command **'cd -'** changes to the previous directory; where the user was previously to the current directory. The following example illustrates this behavior, switching between two directories, which is useful when processing a series of similar tasks.

  ```bash
  [user@host ~]$ cd Videos
  [user@host Videos]$ pwd
  /home/user/Videos
  [user@host Videos]$ cd /home/user/Documents
  [user@host Documents]$ pwd
  /home/user/Documents
  [user@host Documents]$ cd -
  [user@host Videos]$ pwd
  /home/user/Videos
  [user@host Videos]$ cd -
  [user@host Documents]$ pwd
  /home/user/Documents
  [user@host Documents]$ cd -
  [user@host Videos]$ pwd
  /home/user/Videos
  [user@host Videos]$ cd
  [user@host ~]$
  ```

# Shortcuts

- **Ctrl+Alt+UpArrow/DownArrow** : To switch between workspaces sequentially.
- Useful Command-line Editing Shortcuts


  Shortcut| Description
  --------|-------------------------------------------
  Ctrl+A  | Jump to the beginning of the command line.
  Ctrl+E  | Jump to the end of the command line.
  Ctrl+U  | Clear from the cursor to the beginning of the command line.
  Ctrl+K  | Clear from the cursor to the end of the command line.
  Ctrl+LeftArrow  | Jump to the beginning of the previous word on the command   line.
  Ctrl+RightArrow  | Jump to the end of the next word on the command line.
  Ctrl+R  | Search the history list of commands for a pattern.
  Esc+.   | Copies the last argument of previous commands
  !!      | Execute the last command
  sudo!!  | Execute the last command as super user

# Common Commands

- **ls -R** : To list the contents of all subdirectories too


# Logging in over the Network

- In this example, a user with a shell prompt on the machine host uses ssh to log in to the remote Linux system remotehost as the user remoteuser:

  ```bash
  [user@host ~]$ ssh remoteuser@remotehost
  remoteuser@remotehost password: password
  ```

- In the next example, a user with a shell prompt on the machine host logs in to remotehost as remoteuser using ssh, using public key authentication. The -i option is used to specify the user's private key file, which is mylab.pem. The matching public key is already set up as an authorized key in the remoteuser account.

    ```bash
    [user@host ~]$ ssh -i mylab.pem remoteuser@remotehost
    [remoteuser@remotehost ~]$
    ```

    For this to work, the private key file must be readable only by the user that owns the file. In the preceding example, where the private key is in the mylab.pem file, the command chmod 600 mylab.pem could be used to ensure this.

- **Logging Out:** When you are finished using the shell and want to quit, you can choose one of several ways to end the session. You can enter the exit command to terminate the current shell session. Alternatively, finish a session by pressing **_Ctrl+D_**.

