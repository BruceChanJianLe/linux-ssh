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
ssh-copy-id ~/.ssh/id_cjl remote-user@ip
```
