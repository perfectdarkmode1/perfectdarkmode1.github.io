# Add a permanent home alias in WSL2

Vim
```
vim ~/.bashrc
alias home='cd /mnt/c/Users/david.thomas$' <--- Add this line to file, not a command.
$ source ~/.bashrc
```

# Yank entire file to clipboard in vim

```
sudo apt install vim-gtk3
# open vim
:%y+
```

# Create new user with . in the name
```
add user --force-badname david.thomas
```
and add them to sudoer file
```
sudo usermod -aG sudo david.thomas
```
### Create and edit- `/etc/wsl.conf`

 Ceate a `/etc/wsl.conf` with the following setting:

```
[user]
default=username
```

Changing, of course, username to be your default username.

Exit your distro/instance, then issue a `wsl --terminate <distroname>` from PowerShell or CMD. When you restart, the default user should be set.

This is safer and less error-prone than the registry-based methods.02

