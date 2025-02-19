---
title: "Linux"
description: ""
summary: ""
date: 2024-10-18T20:27:45+08:00
lastmod: 2024-10-18T20:27:45+08:00
weight: 302
draft: false
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

### Linux Distribution

{{< inline-svg src="svgs/logos/linux.svg" width="100px" height="79px" class="svg-inline-custom" >}}

#### Ubuntu

{{< inline-svg src="svgs/logos/ubuntu.svg" width="100px" height="79px" class="svg-inline-custom" >}}

Debian Linux based OS, comes with preloaded packages

#### Arch

{{< inline-svg src="svgs/logos/archlinux.svg" width="100px" height="79px" class="svg-inline-custom" >}}

DIY. Arch Linux is ideal for experienced users

### Terminal Command-Line Basics

```bash
man ls  # List manual

ls    # List directory
ls -l # Shows more details
ls -a # Shows hidden 
ls -h # Shows human readable info

tree        # Show all files and folders in the current directory
tree /path  # Show the structure of a specific directory.
tree -L 2   # Limit the depth of displayed subdirectories to 2 levels.
tree -d     # Show only directories
tree -f     # Show the full path 

cd        # Change directory
cd ..     # Move to parent directory
cd ~      # Move to home
cd <tab>  # View suggested inputs
pwd       # Print working directory full path

touch file.txt  # Create file
mkdir dir       # Make directory
rm file.txt     # Remove file
rmdir           # Remove directory
cp test.txt ~/Downloads # Copy file
mv test.txt ~/Downloads # Move file/rename file

cat -n file.txt   # Concatenate and display file content.


chmod +x script.sh  # Grant execute permission to a file
chmod go-rwx file   # Restrict permissions for a file

chown user:group file # Change the owner of a file
chown -R user:group directory # Change the owner of a directory and its contents recursively

ps      # Display currently running processes.
ps aux  # List all processes
ps -u username  # Show processes of a specific user

kill PID  # Terminate processes by ID or name.

tar -czvf archive.tar.gz directory  # Create a compressed archive
tar -xzvf archive.tar.gz -C /path/to/destination # Extract an archive to a specific directory

gunzip *.gz # Decompress multiple files with a wildcard

wget URL # Retrieve files from the internet.

scp user@remote:/path/to/file /local/path # Copy a file from a remote server to local machine
scp -r /local/directory user@remote:/remote/path # Copy a directory from local to remote
scp file.txt user@remote:/path # Copy a file from local to remote

ssh -i /path/to/private_key user@host # Connect to a server using a specific private key
ssh -L 8080:localhost:80 user@host # Establish an SSH tunnel for port forwarding

ifconfig    # Display network interface information.
ifconfig -a # List all network interfaces

sudo ifconfig eth0 192.168.1.2 netmask 255.255.255.0 # Set an IP address for a specific interface

netstat # Display network connections
netstat -tulnp # Show all listening ports
netstat -s # Display statistics for a specific network protocol

sudo route add -net 192.168.1.0 netmask 255.255.255.0 gw 192.168.0.1 # Add a new route to the routing table
sudo route del -net 192.168.1.0 netmask 255.255.255.0 # Delete a specific route

ping google.com # Test network connectivity to a host
ping -i 2 google.com >> ping_log.txt # Ping continuously and record the output to a file

traceroute -m 20 google.com # Trace the path packets take with maximum hops. Alias: tracert

nslookup domain.com # Query DNS servers. Alias: dig

hostname # Display or set system hostname.
sudo hostname temporary_name # Change the hostname temporarily

name -r   # Check kernel version
uname -m  # Show system architecture
uname -s  # Show only the kernel name

whoami # Display current username.
if [ "$(whoami)" != "root" ]; then echo "Please run as root"; fi

df -h # Show available space in human-readable format
df -T /dev/sda1 # Display space usage of a specific filesystem

du -h # Display directory space usage
du -sh directory # Display total size of a directory

find / -mtime -1 # Find files modified within the last 24 hours
find / -user username # Search for files owned by a specific user

systemctl # Control system services.
sudo systemctl enable servicename # Enable a service to start at boot
systemctl status ssh # Check the status of a service

journalctl # Query and display system logs.
journalctl -u servicename # Filter logs for a specific service
journalctl --since "2023-12-01 00:00:00" # Display logs since a specific time

firewall-cmd/ufw # Configure firewall rules.
sudo ufw allow from 192.168.1.100 # Allow all traffic from a specific IP address
sudo ufw default deny incoming # Deny all incoming traffic by default

lsof # List open files and processes.
lsof /path/to/file # List processes using a specific file
lsof -i # Show network-related processes

tcpdump # Network packet analyzer.
sudo tcpdump -i eth0 # Capture packets on a specific interface
sudo tcpdump -i eth0 port 80 # Display HTTP traffic

netcat (nc) # Network utility for reading and writing data across network connections.
nc -l -p 1234 # Create a simple TCP server
nc -l -p 1234 < file.txt # Transfer files between systems

ssh-keygen # Create SSH key pairs for secure authentication.
ssh-keygen -t rsa # Generate an RSA key pair
ssh-keygen -t rsa -f /path/to/key # Create a key pair with a specific filename

ssh-copy-id # Copy SSH keys to a remote server.
ssh-copy-id user@host # Copy the public key to a remote host
ssh-copy-id -p port user@host # Use a specific port for copying the key

rsync # Remote file synchronization and transfer.
rsync -avz /source user@remote:/destination # Synchronize files and directories between local and remote
rsync -av --delete /source user@remote:/destination # Delete files at the destination that are not in the source

tail # Display the last part of a file.
tail file.txt # View the last 10 lines of a file
tail -f log.txt # Continuously display new lines appended to a file

head # Display the beginning of a file.
head -n 15 file.txt # Display a specific number of lines from the start


echo "Hello, World!" # Print a message
variable="value"; echo $variable # Assign a value to a variable
echo "Content" > file.txt # Output text to a file
echo "More content" >> file.txt # Append text to a file

date -u # Display date and time in UTC
date +"%Y-%m-%d %H:%M:%S" # Display date and time in a specific format

curl URL # Retrieve content from a URL
curl -X POST -d "data" URL # Send data via POST request

history # Show the list of recent commands
history | grep "pattern" # Search for commands containing specific text

which # Locate a command.
which command # Find the path of an executable
which ls # Check if a command is available in the system

wc # Display line, word, and character count for a file.
wc -l file.txt # Count lines in a file
wc -w file.txt # Count words in a file

uniq # Report or omit repeated lines in a file.
sort file.txt | uniq # Show unique lines in a sorted file
sort file.txt | uniq -c # Display count of occurrences for unique lines

sort # Sort lines of text files.
sort file.txt # Sort lines in a file
sort -n file.txt # Sort lines numerically

alias # Create shortcuts for commands.
alias ll='ls -l' # Create an alias for a command
alias # List all defined aliases

diff # Compare files line by line.
diff file1.txt file2.txt # Compare two files and display differences
diff -r dir1/ dir2/ # Show differences between two directories

gzip # Compress files.
gzip file.txt # Compress a file
gzip file1 file2 # Compress multiple files
gzip *.txt # Compress multiple files using wildcards

uptime # Show how long the system has been running.
uptime # Display system uptime
uptime -p # Show load average for the last 1, 5, and 15 minutes
```

You can use the pipe symbol (|) to pass the output of one command as the input of another command. For example, ls -l | grep txt will list only the files that have the txt extension.

You can also use the redirection symbols (> and <) to redirect the output or input of a command to a file. For example, echo "Hello World" > hello.txt will create a file named hello.txt and write Hello World to it.

#### Grep

This command is useful for filtering things

```bash
grep: Search for patterns in files.

grep "word" file.txt          # Find word in a file
grep -r "pattern" /path/to/   # Search recursively in directories for a specific pattern
grep -c "pattern" file1 file2 # Count occurrences of a pattern in multiple files
grep -v "pattern" file.txt    # Display lines that do not match a pattern
```

Source: [Linux Terminal](https://wirekat.com/how-to-use-the-terminal-in-linux/), [FreeCodeCamp](https://www.freecodecamp.org/news/the-linux-commands-handbook/)

#### Teletype

`tty` stands for teletype, and it refers to a terminal or command-line interface that allows users to interact with the system.

```bash
tty # Show the current terminal name.
who # List logged-in users and their terminals.
echo "Hello" > /dev/tty1 # Send text to a specific terminal.
```

### Basic Concepts

#### Linux shell

A shell connects user to the system through terminal. Automate tasks using shell scripts. Scripts is a file which tells the shell to execute in order. Linux-based system use `.sh` for script file, Windows use `.ps1` for powershell and `.bat` or `.cmd` for command prompt, cross-platform python use `.py`

```bash {title="hello.sh"}
#!/bin/bash   # This is shebang, to tell system to use bash interpreter.
echo "Hello World!" 
```

| Shell | Description |
| - | - |
| Bash (Bourne Again Shell) | Default on many Linux systems. |
| Zsh (Z Shell) | Enhanced with more features and better scripting. |
| Fish (Friendly Interactive Shell) | User-friendly with autosuggestions.  |
| Dash, Ksh, Csh, Tcsh | Other alternatives. |

#### Permissions

File have to change it's permission to enable execution. `r` read 4, `w` write 2, `x` write 1, `u` owner, `g` group, `o` others

```bash
# Change mode

chmod 755 file.txt  # rwxr-xr-x (Owner: read/write/execute, Group & Others: read/execute)
chmod u+x file.sh   # Add execute permission to owner
chmod g-w file.txt  # Remove write permission for group
chmod o= file.txt   # Remove all permissions for others
```

```bash
# Change owner

chown nut17 file.txt          # Change owner to nut17
chown nut17:developers file.txt # Change owner to alice and group to developers
sudo chown -R nut17 /var/www    # Recursively change owner of all files in directory
```

```bash
# User File Creation Mask

chown alice file.txt          # Change owner to alice
chown alice:developers file.txt # Change owner to alice and group to developers
sudo chown -R bob /var/www    # Recursively change owner of all files in directory

```

chmod, chown, umask.

#### Processes
Process Management: ps, top, kill, jobs, bg, fg.

#### Shell Scripting
Basic scripting with bash or sh.
Variables, loops, and conditionals: if, for, while.
Handling input/output: read, redirection (>, >>, <), piping (|).

#### Package Management
Debian-based: apt, dpkg.
RedHat-based: yum, dnf, rpm.
Universal: snap, flatpak.

#### Filesystem Knowledge
File hierarchy: /home, /etc, /var, /tmp, /usr, /proc.
Mounting drives: mount, umount.
Disk space management: df, du.

#### Networking Basics
Checking connections: ping, curl, wget.
Debugging: netstat, ss, traceroute.
Setting up SSH: ssh, scp, rsync.

#### Environment Management
Environment variables: export, .bashrc, .profile.
Aliases and functions for frequently used commands.

#### System Performance Monitoring
Resource usage: htop, vmstat, iostat.
Log analysis: tail, less, /var/log.

#### Build Tools
Compilers: gcc, g++.
Makefiles: make, cmake.

#### Software Development Tools
Docker basics: docker run, build, compose.
Virtual environments: venv (Python), nvm (Node.js).
Debugging tools: gdb, strace.
Let me know if you’d like examples or deeper insights into any of these.

