# Install Alpine linux in a VM and set up as a Docker host

- Download ISO:  [here](https://alpinelinux.org/downloads/)
- Create a VM and point the optical drive to the ISO.  Set NIC to bridged adapter.
- Start the VM.
- Login as 'root'.  No password required.
- Run `setup-alpine`.
- For keyboard, enter 'us' and then 'us'.
- Enter a suitable host name.
- Accept network defaults.
- Enter a new root password. Pick something secure and easy to remember, like 'password', or '123456'.
- For time zone, enter 'America' and 'Los_Angeles'.
- No proxy.  
- Any mirror will do, I pick '20' for mirror.clarkson.edu. 
- Select defaults of 'openssh', 'chrony'.
- Use 'sda' for installing 'sys'.
- Wait....
- Power off, disconnect iso from optical drive.
- Power on. login as root using the new password.
- Add a new user: `adduser <username>`.  You should now be able to ssh to the VM and login.  The default ssh config
forbids root logins.
-  To install packages, use apk as root.  You may need to edit `/etc/apk/repositories` to enable the community packages.
You will need to use vi or nano as the editor.  For vi, curser down to the comment char(#), backspace, and then `:x` to exit. 
Then run `apk update`.
- Install emacs: `apk add emacs-nox`.
- Install docker: `apk add docker`; to make docker start on boot: `rc-update add docker boot`; to start manually:
`rc-update add docker boot`.
- install java `apk add openjdk8-jre`
- Fetch and run a docker container.  For example, to run cassandra (latest build) in a container named 'entity-resolution':
`docker run --name entity-resolution -d cassandra:latest`.  





