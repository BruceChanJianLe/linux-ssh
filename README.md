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
# Edit /etc/ssh/ssh_config
sudoedit /etc/ssh/ssh_config
# Activate single authentication
# Add the lines below Host *
Host *
    ControlMaster auto 
    ControlPath ~/.ssh/%r@%h:%p
```

Remember to reset SSH service for changes to update.
```bash
sudo systemctl restart ssh
```
