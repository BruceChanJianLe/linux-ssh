# Linux SSH

This repository stores notes on using ssh.

## Usage

### Create SSH Key Pair

```bash
# Follow the instructions to create the key to ~/.ssh directory
ssh-keygen -t ed25519 -C "jianle001@e.ntu.edu.sg"
# To ensure newly created key is acknowledge ssh agent
ssh-add
```

### Password-less Remote Access

```bash
ssh-copy-id -i ~/.ssh/id_cjl.pub username@remote_server_ip
```

Sometimes, even after running `ssh-copy-id`, the remote server still
prompts for you to input password. This can happen if your local machine
does not know which identity file to use. An easy check would be:  

```bash
ssh-add -l
```

If the about result is empty or does not contain the identity file
that you added to the remote server, this means that you will need
to tell your local machine manaully.  

Don't fred, run the below command to add your identity file and try
again :D  

```bash
ssh-add .ssh/id_cjl```

### Pasword-less Remote with Sudo

```bash
# SSH to remote target
ssh username@remote_server_ip
```

```bash
# Edit the sudoer file with your favourite editor
sudoedit /etc/sudoers
# Add rule for your sudo access
yourusername    ALL=(ALL:ALL) ALL
```

```bash
# Save, exit and try
sudo -l
```

### SSH for Speed

One way to speed up the ssh session is to use the same
encrypted tunnel instead of having each authenticate again.
```bash
# Edit ~/.ssh/config
nvim ~/.ssh/config
# Add the lines below
Host *
    ControlMaster auto 
    ControlPath ~/.ssh/%r@%h:%p
```

### Restarting SSH Service

```bash
sudo systemctl restart ssh
```

### SSH Cipher

Listing the available ciphers.
```bash
sudo sshd -T | grep ciphers
```

Using a specific cipher.
```bash
ssh -c blowfish username@remote_server_ip
```

### SSH with Compression

Compression may or may not speed up the session,
but it may be worth to try.
```bash
ssh -C -c blowfish username@remote_server_ip "find /"
# Timing your ssh session
time ssh -C -c blowfish username@remote_server_ip "find /"
```

### SSH -X

Sometimes you might wanna display GUI when performing ssh,
you can achieve that by running:

```bash
# For example
ssh -X remote_user@192.16.10.110
```

And sometimes, your ssh session can mess up. Resulting in a
situation where you cannot copy things from within the terminal.


In such cases, you will need to export two variables for it to work again.
Of course, I assume that it is working the first time.

```bash
export DISPLAY=localhost:10.0
export XAUTHORITY=~/.Xauthority
```

Now you should be able to copy directly from your terminal again :D
