
# Setting Up The WeeWX RSYNC Uploader

The Reference => StdReport => RSYNC section in the docs has the following sentence:

  _"If you wish to use rsync, you must configure passwordless ssh using public/private key authentication from the user account that WeeWX runs, to the user account on the remote machine where the files will be copied."_

Understanding how to set up passwordless ssh can be difficult for new users to learn.

## How The RSYNC Uploader Works

The WeeWX RSYNC uploader uses the rsync protocol over a ssh transport layer, using passwordless key pairs.  What this means is the WeeWX computer needs to be able to ssh into the desired remote server, without any prompts for a username or password.  A one-time setup is required.

This example will walk you through how to do so, step-by-step, validating each step has been completed successully before proceeding to the next step.  Complete setup should ideally take just a few minutes of your time.

## What Is Needed

The short list of what is needed is:

* the WeeWX user needs to generate a passwordless public/private key pair
  * for a packaged installation, this is user 'weewx'
  * for a pip installation, this is the user you use for the venv

* the remote server account needs to be configured to accept the 'public' key from the WeeWX account
  * `$HOME/.ssh/authorized_keys file` needs an entry for the WeeWX account's public key

* the WeeWX user needs to trust that the remote server is indeed the desired remote server, and not a man-in-the-middle
  *  the remote computer's 'host' key needs to be in the WeeWX account's `$HOME/.ssh/known_hosts` file

* at that point, you need to edit `weewx.conf` to set up the `[RSYNC]` stanza, then restart WeeWX

## How To Set It Up

This is an example of setting up passwordless ssh for WeeWX's rsync uploader.

In this test:
 * the local host is a mac mini named 'mini'
 * the local user is 'vince' with home directory '/Users/vince'
 * the remote host is named 'pi4jr'
 * the remote user is 'pi' with home directory '/home/pi'
 * we want to upload to the remote path '/home/pi/from_mac_mini'
 * this example names the keypair 'id_weersync_test'

### (1) Log in as the WeeWX user on the WeeWX computer

If you run a 'pip' installation, this is the user you created the venv under.  Simply open a terminal shell.

If you run a packaged installation, this is user 'weewx' but this account set does not permit interactive logins. To get around this, we need to use `sudo` to open the required shell by running `sudo -u weewx bash`.  Then run `id -un` and `id -gn` which should both report `weewx` as your user and group.


### (2) Generate a public/private keypair

Next run `ssh-keygen` to create a public/private key pair.  Take the defaults.  Optionally specify a filename you want to use for the keypair so that your have a keypair for WeeWX rsync operations only.

The remainder of this example assumes you will name the keypair.

````
[vince@mini ~]$ ssh-keygen
Generating public/private ed25519 key pair.
Enter file in which to save the key (/Users/vince/.ssh/id_ed25519): /Users/vince/.ssh/id_weersync_test
Enter passphrase for "/Users/vince/.ssh/id_weersync_test" (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /Users/vince/.ssh/id_weersync_test
Your public key has been saved in /Users/vince/.ssh/id_weersync_test.pub
The key fingerprint is:
SHA256:fIWp5f9FuhpXlQ2SORpx7RFxNXVCQ1PzhquDYHcbp48 vince@mini
The key's randomart image is:
+--[ED25519 256]--+
|          ..o*X*O|
|          .++.oBB|
|          +o.o.o=|
|       . +..  .o.|
|        S + o o o|
|       . + + * + |
|          . B o .|
|             B o |
|            E.+  |
+----[SHA256]-----+
````

### (3) Authorize the specified key on the remote account@system

You may get a one-time prompt asking you to ok that the
remote system is the host you think it is.  Answer 'yes'
to make it a known_host in your local ~/.ssh/known_hosts file

You will then be prompted for the remote user password.
When the ssh-copy-id has completed successfully, the
specified key is set up on the remote server.

````
[vince@mini ~]$ ssh-copy-id -i $HOME/.ssh/id_weersync_test pi@pi4jr

/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/Users/vince/.ssh/id_weersync_test.pub"
The authenticity of host 'pi4jr (192.168.1.164)' can't be established.
ED25519 key fingerprint is SHA256:VZ7JsiK4OwFhu8BakNFBRn8wGJq2PpDizkuSv7JxXbE.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
pi@pi4jr's password:

Number of key(s) added:        1
````

### (4) Test that the passwordless keypair works if it is specified

A successful test does not prompt for a password.

````
[vince@mini ~]$ ssh -i $HOME/.ssh/id_weersync_test pi@pi4jr
Linux pi4jr 6.12.47+rpt-rpi-v8 #1 SMP PREEMPT Debian 1:6.12.47-1+rpt1 (2025-09-16) aarch64
Last login: Fri Dec 26 14:56:09 2025 from 192.168.1.51

pi@pi4jr:~ $
logout
Connection to pi4jr closed.
````

### (5) edit your ~/ssh/config file and add an entry for your remote host

For hostname, use the hostname you used above. For this example, the file would contain.

````
host pi4jr
 hostname pi4jr
 user pi
 identityfile ~/.ssh/id_weersync_test
````

### (6) test that the passwordless keypair works without needing to specify the key name

A  successful test does not prompt for a password

```
[vince@mini ~]$ ssh pi4jr
Linux pi4jr 6.12.47+rpt-rpi-v8 #1 SMP PREEMPT Debian 1:6.12.47-1+rpt1 (2025-09-16) aarch64
Last login: Fri Dec 26 15:07:04 2025 from 192.168.1.51

pi@pi4jr:~ $
logout
Connection to pi4jr closed.
````

### (7) edit weewx.conf file to set up the RSYNC uploader

Use the remote server name or ip you specified above

````
[[RSYNC]]
  server = pi4jr       # remote host alias in ~/.ssh/config
  user = pi                          # remote user in the ~/.ssh/config
  path = /home/pi/from_mac_mini      # remote path to upload to
  enable = true                      # enable the rsync uploader

````

### (8) Test the RSYNC uploader works

For a 'pip' installation of WeeWX, remember to activate your venv as always by running `source ~/weewx-venv/bin/activate`.

A successful test does not prompt you for a password.

````
[vince@mini ~]$ weectl report run RSYNC
Using configuration file /Users/vince/weewx-data/weewx.conf
The following reports will be run: RSYNC
Generating as of last timestamp in the database.
Done.
````

As a final check, verify your WeeWX `public_html` tree was indeed copied to the remote server.

### AT THIS POINT YOUR SETUP IS COMPLETE

Restart WeeWX and the rsync handler should work when
your next report interval occurs.  Check your remote
system and your WeeWX logs to be certain.


