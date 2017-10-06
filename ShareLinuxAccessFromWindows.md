# Create a Share on Linux and Access It from Windows (from [How To-Geek](https://www.howtogeek.com/176471/how-to-share-files-between-windows-and-linux/))

Creating a share on Linux and then accessing it from Windows is actually a bit easier than the other way around. First, we’ll create the shared folder on the Linux system. Then, we’ll look at how to access it from a Windows PC.

## Step One: Create the Share on Linux

To set up a shared folder on a Linux that Windows to access, start with installing Samba (software that provides access to SMB/CIFS protocols used by Windows). At the terminal, use the following command:
```
sudo apt-get install samba
```
After Samba installs, configure a username and password that will be used to access the share:
```
sudo smbpasswd -a <user_name>
```
_Note: In this example, <user_name> can be a Linux user, but you can choose any name you’d like._

Use a directory that exists or create another one. Here we're going to use a directory named `share`.
```
mkdir ~/share
```
Now, configure the smb.conf file.
```
sudo vi /etc/samba/smb.conf
```
Scroll down to the end of the file and add these lines:
_replace <user_name> with your personnal setting_
```
[share]
path = /home/<user_name>/share
available = yes
valid users = <user_name>
read only = no
browsable = yes
public = yes
writable = yes
```
Now, you just need to restart the SMB service for the changes to take effect.
```
sudo service smbd restart
```
Your shared folder should now be accessible from a Windows PC.

## Step Two: Access the Linux Share from Windows

Now, let’s add the Linux share to our Windows Desktop.  Right-click somewhere on your Desktop and select New > Shortcut.

Type in the network location of the shared folder, with this syntax:

\\IP-ADDRESS\SHARE-NAME

```
\\192.168.0.13\share
```

Note: If you need the IP of your Linux computer, just use the `ifconfig` command at the terminal.

In the shortcut wizard on the Windows PC, click Next, choose a name for the Shortcut, and then click Finish. You should end up with a Shortcut on your Desktop that goes right to the Linux share.
