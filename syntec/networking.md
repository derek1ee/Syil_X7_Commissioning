# Syntec 22MA networking & workflow

There are several ways to load NC programs to the controller, in addition to using a USB key. These methods can be divided into two categories.

* Controller pull
* Computer push

## Controller pull
The controller is connected to local network, and can access a remote file share to pull NC programs from.
This is available either via computer operating system/NAS’ built-in SMB sharing protocol, or by using Syntec’s “FS Server” application (available only on Windows).

The workflow looks like the following:
1. From CAM software, post to either a local directory that’s shared, or to a NAS drive.
1. On the controller, go to File Manager, then File Transfer. Select “network” as the source (instead of USB drive), then select destination, and copy.

## Computer push
The controller is connected to the local network, and the storage is made available on the network for computers to directly post NC programs to.
This is my preferred method, because it doesn’t require me to go through the “File Transfer” process on the controller.
However, Syntec controllers only make storage available via FTP, rather than as a network drive. And Windows OS cannot map an FTP location as a drive number.
Fusion also can’t post directly to an FTP server.
Instead, 3rd party software is required:
1. I use WinSCP, which is free. 
1. Obtain Syntec controller’s IP address by going to “Maintaince”, “Set kernel server”.
1. Open WinSCP, and establish a connection to the IP address from above, there’s no username/password required.
1. Create an empty folder on your computer, this folder will be synchronized with the controller’s storage, and will be where you post to from Fusion/CAM.
1. In WinSCP, go to “Commands”, “Keep remote directory up to date”. Select the folder you created above as the local directory to watch, and select the root directory of the remote directory to sync. You will want to make sure to check “Update subdirectories” if you use folders to organize your code (NOTE: Syntec only supports 1 level of sub folder), “Use same options next time”, and “Synchronize on start”. Optionally, you may also want to check “Delete files” if you want to be able to delete files from the controller by deleting them on your computer’s folder. You will want to make sure to uncheck “Existing files only”. Read more about the WinSCP feature here.
1. Once it starts, you can minimize the window and it will keep monitoring and keep the folder & controller in sync.

With this approach, the workflow will look like:
1. From CAM, post to the local folder.
1. Go to the controller, open file manager, locate the file, and execute.
