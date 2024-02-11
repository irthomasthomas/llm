- [] Link context to a terminal if run interactively.

You can use the `tty` command to get the terminal device file associated with the current terminal session. You can then use this device file to tie an entity to a particular terminal session.
To check the tty of the current terminal session, run the following command:
```
tty
```
This will output the device file associated with the current terminal session, such as `/dev/pts/0`.
You can then use this device file to tie an entity to the terminal session, for example by storing it in a configuration file or using it as a key in a database.

- [] Daemon mode: run in the background and tie to a terminal.
  
I cannot store the tty in the database because it is ephemeral. Options, therefore, are to store it in a temporary file or lock file, or to run as a daemon and keep the tty:conversation_id in memory.
File locking is a good option, but it is not portable across different filesystems. It is also not a good option for a daemon, because the lock file would have to be constantly checked and updated. This would be a waste of resources. 

The best option is to run as a daemon and keep the tty:conversation_id in memory. This way, the tty:conversation_id is tied to the terminal session and can be accessed by the daemon when needed. This approach is more efficient and portable than using file locking. This has the added benefit of allowing the application to respond faster to user input, as it is always running in the background and ready to process requests. 
