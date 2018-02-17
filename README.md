# rmIcon
Removes `Icon?` file from Dropbox, left by macOS. Runs on login, and every 10 minutes. 


## The Problem

macOS creates `.Icon?` files that contain information about a file's icon. This is typically a dot file (hidden), but sometimes Dropbox doesn't handle them properly. The result is a hidden file `Icon?` (without the dot). 

This leads to strange behavior -- 

The file `Icon?` appears:
*__When viewing the Dropbox folder as a Stack in the Dock__
*In the terminal (ls output)
*In a Finder window showing hidden files

The file `Icon?` does not appear:
*In a normal Finder window


## Instructions






## FAQ 

1. Why touch then rm?
### Disclaimer:

(Title) is not affiliated with or otherwise sponsored by Dropbox, Inc.
