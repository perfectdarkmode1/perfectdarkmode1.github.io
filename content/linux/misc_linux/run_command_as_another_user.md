---
title: Run Command as Another User
draft: true
---

To invoke a login shell using `sudo` just use `-i`. When command is not specified you'll get a login shell prompt, otherwise you'll get the output of your command.

Example (login shell):

```bash
sudo -i
```

Example (with a specified user):

```bash
sudo -i -u user
```

Example (with a command):

```bash
sudo -i -u user whoami
```

Example (print user's `$HOME`):

```bash
sudo -i -u user echo \$HOME
```

Note: The backslash character ensures that the dollar sign reaches the target user's shell and is not interpreted in the calling user's shell.

I have just checked the last example with _strace_ which tells you exactly what's happening. The output bellow shows that the shell is being called with `--login` and with the specified command, just as in your explicit call to bash, but in addition _sudo_ can do its own work like setting the `$HOME`.

```bash
# strace -f -e process sudo -S -i -u user echo \$HOME
execve("/usr/bin/sudo", ["sudo", "-S", "-i", "-u", "user", "echo", "$HOME"], [/* 42 vars */]) = 0
...
[pid 12270] execve("/bin/bash", ["-bash", "--login", "-c", "echo \\$HOME"], [/* 16 vars */]) = 0
...
```

I noticed that you are using `-S` and I don't think it is generally a good technique. If you want to run commands as a different user without performing authentication from the keyboard, you might want to use SSH instead. It works for `localhost` as well as for other hosts and provides public key authentication that works without any interactive input.

```bash
ssh user@localhost echo \$HOME
```

Note: You don't need any special options with SSH as the SSH server always creates a login shell to be accessed by the SSH client.