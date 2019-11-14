# rmIcon
A shell script that removes the file `Icon?` file from Dropbox, created by macOS and corrupted by Dropbox. When used with the LaunchAgent, it runs on login  and then every 10 minutes. 


## The Problem

When you change a folder's icon, macOS creates a `.Icon?` file that contains that information. This should be a dot file (hidden), but sometimes Dropbox doesn't handle them properly. The result is an `Icon?` file (hidden flag enabled, but without the dot). 

Rightfully,  

The `Icon?` file does not appear:
- In a normal Finder window

And the `Icon?` file does appear:
- In the terminal (`ls -a` output)
- In a Finder window showing hidden files

__But, strangely, The `Icon?` file does appear (wrongfully):__ 
- __When viewing the Dropbox folder as a Stack in the Dock__

This is what I aimed to fix.

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

When the shell script starts, it pauses for 20 seconds then removes the unwanted `Icon?` file. 


## FAQ 

__1. Why `touch` then `rm`?__

  On my machine, I can `rm` the file manually in the Terminal, but for some reason the script doesn't recognize that the file exists when using `rm`. Using `touch` first creates an identical file, then `rm` can delete both of them. I'm honestly not sure why this happens, I just tinkered until I found something that worked but didn't risk deleting other files. 



### Disclaimer:

rmIcon is not affiliated with or otherwise sponsored by Dropbox, Inc.
