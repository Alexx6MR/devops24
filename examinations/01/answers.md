## QUESTION A

What are the permissions of the `~/.ssh` directory?

**Answer:** The Owner has **(rwx)** read, write, and execute permissions but the others group does not have any permission at all.

Why are the permissions set in such a way?

**Answer:** The permissions are set this way to ensure security and privacy of your SSH keys and configuration files.

## QUESTION B

What does the file `~/.ssh/authorized_keys` contain?

**Answer:** 
The file `~/.ssh/authorized_keys` contian the public keys that are authorized to access a user's account.

**Output**:
```bash
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAILNi286YxhuquuAUGnXMbhjVr8+AIUKKmc+pxaBZXnAu deploy key
```

## QUESTION  C

When logged into one of the VMs, how can you connect to the
other VM without a password?

**Answer:** If I want to connect to another virtual machine from within a virtual machine, I have to copy the `shh_key` public key that I already have on my host machine to the `~/.ssh/` folder inside the virtual machine and make sure it has the correct privileges to be used.

## BONUS QUESTION 

Can you run a command on a remote host via SSH?

**Answer:** Yes, you can run a command on a remote host via SSH.

How?

**Answer:**
template: ssh destination -t 'command; bash -l'

example:
```bash
ssh webserver -t 'echo "hello world"; bash -l'
```
> the **;** is very important to separate the command from the bash.
- `-t`: The flag forces a terminal to be able to interact with the remote bash.
- `echo "hello world"`: the command we want to execute.
- `bash -l`: opens an interactive login shell.