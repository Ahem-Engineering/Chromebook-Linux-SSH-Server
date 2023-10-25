# Chromebook-Linux-SSH-Server
How to enable an SSH Server on a Chromebook running the Linux Development Environment

from your linux terminal:

1) Open ssh config file
   `vi /etc/ssh/sshd_config`

   find the line with `#Port 22`
   press 'i' to enter interactive move. Remove the # and change the port to something above 1024. I used port 2222.

   it should now read something like `Port 2222`
   press escape, then type :wq and press enter.

2) Remove the ssh_not_to_be_run file
   `mv /etc/ssh/ssh_not_to_be_run /etc/ssh/ssh_not_to_be_run.bak`

3) Restart the service
   `systemctl restart ssh`

   you may want to restart the container instead (this is more reliable):
   press Find + Esc keys to bring up the chromebook task manager, now select 'Linux Virtual Machine: termina' and press end process.

4) Go to a machine you wish to ssh into the chromebook and generate a new ssh key. I sshed into my other computer (a mac) and used `ssh-keygen -t rsa` to create a key set in my ~/.ssh/ folder, then ran `cat ~/.ssh/id_rsa.pub`. I then copied the output excluding the host information at the end (i.e. you@localhost...). you may want to copy this file to a usb to transfer it over, email it to yourself and open it on your chromebook.

5) On your chromebook create a file called "authorized_keys" in your local .ssh folder and place the key in it.
   `echo "ssh-rsa <key>" >> ~/.ssh/authorized_keys`
   you can paste your key by right clicking (two finder tap on trackpad) the terminal window.

7) Enable port forwarding for the port you selected earlier by clicking the time in the bottom right of the screen then selecting the settings cog. select advanced > Linux development environment > Port forwarding > add. Add the port you added to the config file earler and if you wish give it a name, like 'SSH-server'. Click add.

8) Log in using the computer you created the keys on by running `ssh -p <port> <login>@<IP>`
   replacing with your chromebook's details.

## Notes:
- you may need to run some commands as sudo, use as required.
- you may also use sshfs to access files, if you wish.
- results may vary, this is what worked for me as of 15th October 2023 running on a Lenovo IdeaPad Flex 5.
   
   
