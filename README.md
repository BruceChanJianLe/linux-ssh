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
ssh-copy-id ~/.ssh/id_cjl username@remote_server_ip
```

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
