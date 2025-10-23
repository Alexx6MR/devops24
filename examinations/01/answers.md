## QUESTION A

What are the permissions of the `~/.ssh` directory?

**Answer:** The Owner has **(rwx)** read, write, and execute permissions but the others group does not have any permission at all.

Why are the permissions set in such a way?

**Answer:** The permissions are set this way to ensure security and privacy of your SSH keys and configuration files.

## QUESTION B

What does the file `~/.ssh/authorized_keys` contain?

**Answer:** ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAILNi286YxhuquuAUGnXMbhjVr8+AIUKKmc+pxaBZXnAu deploy key

## QUESTION  C

When logged into one of the VMs, how can you connect to the
other VM without a password?

**Answer:** To set up SSH public‑key authentication from the VM you’re logged into the other VM.

## BONUS QUESTION 

Can you run a command on a remote host via SSH? How?

**Answer:** Yes, you can run a command on a remote host via SSH.