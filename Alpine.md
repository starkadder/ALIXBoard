# Install Alpine linux in a VM and set up as a Docker host

- Download ISO:  [here](https://alpinelinux.org/downloads/)
- Create a VM and point the optical drive to the ISO.  Set NIC to bridged adapter.
- Start the VM 
- Login as 'root'.  No password required.
- Run 'setup-alpine'
- For keyboard, enter 'us' and then 'us'
- Enter a suitable host name
- Accept network defaults
- Enter a new root password. Pick something secure and easy to remember, like 'password', or '123456'.
- For time zone, enter 'America' and 'Los_Angeles'
- No proxy.  
- Any mirror will do, I pick '20' for mirror.clarkson.edu 
- Select defaults of 'openssh', 'chrony'
- Use 'sda' for installing 'sys'
- Wait....
- Power off, disconnect iso from optical drive.
- Power on. login as root using the new password
- add a new user: `adduser <username>`.  You should now be able to ssh to the VM and login.  The default ssh config
forbids root logins.
-  to install packages, use apk.  You may need to edit `/etc/apk/repositories` to enable the community packages.
You will need to use vi or nano as the editor.  for vi, curser down to the comment char(#), backspace, and then `:x` to exit.  
Then run `apk update`
- install emacs: `apk add emacs-nox`
- install docker: `apk add docker`



