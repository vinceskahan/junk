
# Setting Up The WeeWX RSYNC Uploader

The Reference => StdReport => RSYNC section in the docs has the following sentence:

  _"If you wish to use rsync, you must configure passwordless ssh using public/private key authentication from the user account that WeeWX runs, to the user account on the remote machine where the files will be copied."_

Understanding how to set up passwordless ssh can be difficult for new users to learn.

## How The RSYNC Uploader Works

The WeeWX RSYNC uploader uses the rsync protocol over a ssh transport layer, using passwordless key pairs.  What this means is the WeeWX computer needs to be able to ssh into the desired remote server, without any prompts for a username or password.  To set this up, a few 'one time' steps are required.

### What Is Needed

The short list of what is needed is:

* the WeeWX user needs to generate a passwordless public/private key pair
  * for a packaged installation, this is user 'weewx'
  * for a pip installation, this is the user you use for the venv

* the remote server account needs to be configured to accept the 'public' key from the WeeWX account
  * $HOME/.ssh/authorized_keys file needs an entry for the WeeWX account's public key

* the WeeWX user needs to trust that the remote server is indeed the desired remote server, and not a man-in-the-middle
  *  the remote computer's 'host' key needs to be in the WeeWX account's $HOME/.ssh/known_hosts file

### How To Set It Up

1. Log in as the WeeWX user on the WeeWX computer
    a. if you run a packaged installation, this is user 'weewx'
    b. if you run a 'pip' installation, this is the user you created the venv under

      For pip installations only:
       The 'weewx' user in v5 has its account set to not permit interactive logins, so you need to use sudo (as root) to open the required shell
     
       To do this:  'sudo -u weewx bash' which will open a shell as user 'weewx'
                   then do the remaining local steps and 'exit' to close the shell
     

2. Generate a public/private keypair for WeeWX RSYNC transactions and name it something that makes sense to you

```
# use sudo to open a shell as user weewx
$ sudo -u weewx bash

# check the shell is indeed user 'weewx' group 'weewx'
weewx@nuc2:~$ id
uid=1234(weewx) gid=1234(weewx) groups=1234(weewx),100(users)

# generate a keypair, naming the filenames something obvious to you
weewx@nuc2:~$ ssh-keygen
Generating public/private ed25519 key pair.
Enter file in which to save the key (/home/weewx/.ssh/id_ed25519): /home/weewx/.ssh/id_ed25519_weewx_rsync
Created directory '/home/weewx/.ssh'.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/weewx/.ssh/id_ed25519_weewx_rsync
Your public key has been saved in /home/weewx/.ssh/id_ed25519_weewx_rsync.pub
The key fingerprint is:
SHA256:32R0rQvE3UEh13tFHhaHXiWdBqwXHrv/eFmi5HFGxvg weewx@nuc2
The key's randomart image is:
+--[ED25519 256]--+
|            .o+%X|
|           . ==BO|
|            *+B.*|
|           +.==o.|
|        S   =+o .|
|         . +ooE..|
|          .o.=o.o|
|            o  +.|
|              ..o|
+----[SHA256]-----+

# the result is you have a keypair under weewx's home directory
weewx@nuc2:~$ ls -alg /home/weewx/.ssh
total 16
drwx------ 2 weewx 4096 Dec 24 18:18 .
drwxr-x--- 3 weewx 4096 Dec 24 18:17 ..
-rw------- 1 weewx  399 Dec 24 18:18 id_ed25519_weewx_rsync
-rw-r--r-- 1 weewx   92 Dec 24 18:18 id_ed25519_weewx_rsync.pub
```

3. Next, use 'ssh-copy-id' to authorize the keypair on the remote computer

```
# authorize the key, entering the remote account's password when prompted

weewx@nuc2:~/.ssh$ ssh-copy-id -i id_ed25519_weewx_rsync.pub myremoteuser@192.168.1.171
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "id_ed25519_weewx_rsync.pub"
The authenticity of host '192.168.1.171 (192.168.1.171)' can't be established.
ED25519 key fingerprint is SHA256:TK3TA6mOcRe7kYq2Z/UfgvmzHlPtVTx4UcLTiwdgwR8.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
myremoteuser@192.168.1.171's password:

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh 'myremoteuser@192.168.1.171'"
and check to make sure that only the key(s) you wanted were added.

# verify it indeed works. Since we named the keypair we need the -i parameter in this test
weewx@nuc2:~/.ssh$ ssh -i id_ed25519_weewx_rsync myremoteuser@192.168.1.171
Welcome to Ubuntu 24.04.3 LTS (GNU/Linux 6.8.0-83-generic x86_64)
Last login: Wed Dec 24 18:15:05 2025 from 192.168.1.51

# exit the shell on the remote computer
myremoteuser@nuc2:~$ exit
logout
Connection to 192.168.1.171 closed.

# exit the local weewx shell we sudo'd into
weewx@nuc2:~$ exit
exit
```

4. At this point if you named your keypair you should do a little more configuration so using '-i' in your ssh command is not required

```
# again sudo to open a weewx account bash shell
sudo -u weewx bash

# create a $HOME/.ssh/config
Host my_remote_server x.x.x.x               # create hostname aliases for ssh
IdentityFile ~/.ssh/id_ed25518_weewx_rsync  # use this key specifically
user myremoteuser                           # to this remote user by default
hostname x.x.x.x                            # the name or ip address of the remote system

# make sure the permissions are ok
chmod 600 $HOME/.ssh/config
```

The effect of the above is you should be able to "ssh my_remote_server" or "ssh x.x.x.x" and log right in with no password prompt.  You will need to answer 'yes' once if prompted to trust the remote computer.  The prompt will look something like the following:

```
weewx@nuc2:/$ ssh pi@192.168.1.69
The authenticity of host '192.168.1.69 (192.168.1.69)' can't be established.
ED25519 key fingerprint is SHA256:BR18M3PyFgvHldjnQf/vOdJyWvviL1B5hYQsBkDONlA.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '192.168.1.69' (ED25519) to the list of known hosts.
(and so on)
```

5. Then edit the weewx.conf RSYNC settings per the WeeWX documentation [https://www.weewx.com/docs/5.2/reference/weewx-options/stdreport/#rsync](LINK) and restart weewx to make the changes take effect.

