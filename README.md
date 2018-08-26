# rmIcon
A shell script that removes the file `Icon?` from Dropbox, left by macOS. When used with the LaunchAgent, it runs on login  and then every 10 minutes. 


## The Problem

macOS typically creates `.Icon?` files that contain information about a file's icon. This is typically a dot file (hidden), but sometimes Dropbox doesn't handle them properly. The result is a hidden file `Icon?` (without the dot). 

Rightfully,  

The `Icon?` file does not appear:
- In a normal Finder window

The `Icon?` file appears:
- In the terminal (ls output)
- In a Finder window showing hidden files

__But strangely, The `Icon?` file also appears:__ 
- __When viewing the Dropbox folder as a Stack in the Dock__


## Instructions

Place `com.YOURDOMAIN.rmIcon.plist` in `/Library/LaunchAgents`. Feel free to change "YOURDOMAIN" to whatever you'd like (also change the string within the file). 

Place `rmIcon.sh` in `/Library/LaunchAgents`. 

Run the following commands in Terminal:

```cd /Library/LaunchAgents```

```sudo chown root:wheel rmIcon.sh```

```sudo chown root:wheel com.YOURDOMAIN.rmIcon.plist```

```sudo chmod +x rmIcon.sh```

```launchctl load -w /Library/LaunchAgents/com.YOURDOMAIN.rmIcon.plist```

The Agent should start automatically, but restart your computer for immediate effect. 


## What exactly does this do?

The LaunchAgent loads when a user logs in.

`launchd` runs the shell script immediately when loaded, then once every 10 minutes.

When the shell script starts, it pauses for 20 seconds, removes the unwanted `Icon?` file. 


## FAQ 

__1. Why `touch` then `rm`?__

  On my machine, I can `rm` the file manually in the Terminal, but for some reason the script doesn't recognize that the file exists when using `rm`. Using `touch` first creates an identical file, then `rm` can delete both of them. I'm honestly not sure why this happens, I just tinkered until I found something that worked, but didn't risk deleting other files. 



### Disclaimer:

rmIcon is not affiliated with or otherwise sponsored by Dropbox, Inc.
