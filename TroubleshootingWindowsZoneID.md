## Troubleshooting Windows Zone Identifier 

### Introduction

With the move to a more open source style of development for the AGS engine, game developers may use AGS builds that don't correspond to an official release. These are usually downloaded and extracted manually rather than installed with an installer and this can cause some problems with Windows security settings. Specifically, attempts to access the help file (ags-help.chm) from inside or outside the AGS editor may be blocked (renders a blank page or error).  Additionally, when you download an AGS Editor plugin, it may error when the game project is loaded or the plugin is activated.

This is caused by something called "alternate data streams", and usually right clicking on the file and selecting unblock will fix your problem. Sometimes this doesn't work, so keep reading.


### What are "alternate data streams"?

When a file is stored on a computer by the Operating System it's written in a particular way. In order to read a file back there is a need to know where it begins and ends on the disk, so a File System is used to store data. On Windows the most popular File System is NTFS which supports the use of alternate data streams. Normally the contents of a file will be saved into the NTFS $DATA attribute in the default stream but it is also possible to specify an alternate stream name and store data in a different location within the same file. One common alternate stream name is named "Zone.Identifier" which is used to indicate the Windows Security Zone that a file originates from. This is commonly used to indicate that a file originates from another computer, the origin being indicated by a zone number. The zone numbers are defined by Zone Security settings in Internet Options.

It's typically up to individual web browsers and download utilities running on Windows as to whether they write to the "Zone.Identifier" stream when a file is downloaded, and equally any application could choose to check the "Zone.Identifier" stream of a file when it is being opened. The help file viewer is one such application and will, by default, refuse to open a file if the "Zone.Identifier" indicates it originated from a different computer (i.e. it is potentially unsafe).

When looking at a file's properties, if a restrictive zone number is present in the "Zone.Identifier" stream the file will be listed as "blocked". Choosing to unblock the file will re-write the "Zone.Identifier" stream to indicate the file should not longer be restricted (i.e. programs shouldn't be able to identify the origin of the file


### How do I clean my AGS editor files of "alternate data streams"?

Usually it's just the single "Zone.Indentifier" alternate stream on the help file that causes a problem.


- Right click the ags-help.chm file in Windows Explorer and press the unblock button.

If the unblock button doesn't work this is usually because the AGS folder has been located somewhere where the user attempting to unblock does not have write permission (if this is the case it's likely that the user extracting the AGS Editor would have encountered a UAC prompt when extracting to the AGS Editor files and approved the process to run with elevated permissions). The easiest solution is to run the Windows program "streams.exe" with elevated permissions. It can be download from [here](https://technet.microsoft.com/en-us/sysinternals/bb897440).

- Download the zip file and extract it to any temporary directory, e.g. the Desktop.
- Open a Windows Command prompt using "run-as administrator"
- In the command prompt, change to to directory where the files were extracted:
 `cd "<EXTRACTION FOLDER>"`
  . you need to replace "<EXTRACTION FOLDER>" with the path to where streams.exe was extracted. For example "C:\Users\MyAccount\Desktop\Streams"

 (use double quotes when the path contains spaces)

Run the following command to recursively remove any alternate data streams:

 `streams.exe -s -d "<AGS EDITOR FOLDER>"`
 (you need to replace "<AGS EDITOR FOLDER>" with the path to where the AGS Editor folder was extracted. For example "C:\Users\MyAccount\My Documents\AGS Builds\ags_3.5.0")

 (use double quotes when the path contains spaces)
 
 
An alternate solution is to move the AGS Editor files to a location that doesn't use an NTFS file system, and then move the files back to the computer again. Most USB memory sticks will be formatted with the FAT32 File System instead of NTFS. FAT32 does not support alternate data streams so they cannot exist on the memory stick.