---
title: "Linux"
description: ""
summary: ""
date: 2024-10-18T20:27:45+08:00
lastmod: 2024-10-18T20:27:45+08:00
weight: 402
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

### Linux Concepts

#### Terminal Command-Line Basics

```bash
man ls  # List manual

ls    # List directory
ls -l # Shows more details
ls -a # Shows hidden 
ls -h # Shows human readable info

cd        # Change directory
cd ..     # Move to parent directory
cd ~      # Move to home
cd <tab>  # View suggested inputs
pwd       # Print working directory full path

tree        # Show all files and folders in the current directory
tree /path  # Show the structure of a specific directory.
tree -L 2   # Limit the depth of displayed subdirectories to 2 levels.
tree -d     # Show only directories
tree -f     # Show the full path 

touch file.txt  # Create file
mkdir dir       # Make directory
rm file.txt     # Remove file
rmdir           # Remove directory
cp test.txt ~/Downloads # Copy file
mv test.txt ~/Downloads # Move file/rename file

cat -n file.txt   # Concatenate and display file content.

which # Locate a command.
which command # Find the path of an executable
which ls # Check if a command is available in the system

history # Show the list of recent commands
history | grep "pattern" # Search for commands containing specific text

alias # Create shortcuts for commands.
alias ll='ls -l' # Create an alias for a command
alias # List all defined aliases
```

Source: [Linux Terminal](https://wirekat.com/how-to-use-the-terminal-in-linux/), [FreeCodeCamp](https://www.freecodecamp.org/news/the-linux-commands-handbook/)

#### Grep

This command is useful for filtering things

```bash
grep: Search for patterns in files.

grep "word" file.txt          # Find word in a file
grep -r "pattern" /path/to/   # Search recursively in directories for a specific pattern
grep -c "pattern" file1 file2 # Count occurrences of a pattern in multiple files
grep -v "pattern" file.txt    # Display lines that do not match a pattern
```

#### Teletype

`tty` stands for teletype, and it refers to a terminal or command-line interface that allows users to interact with the system.

```bash
tty # Show the current terminal name.
who # List logged-in users and their terminals.
echo "Hello" > /dev/tty1 # Send text to a specific terminal.
```

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
chmod +x script.sh  # Allow everyone to execute (same as above)
chmod u+x file.sh   # Add execute permission to owner
chmod g-w file.txt  # Remove write permission for group
chmod o= file.txt   # Remove all permissions for others (anyone who is NOT the part of the group assigned to the file)
```

```bash
# Change owner

chown nut17 file.txt          # Change owner to nut17
chown nut17:groupname file.txt # Change owner to a group
sudo chown -R nut17 /var/www    # Recursively change owner of all files in directory
```

For below, the mask is subtracted from the full permission (777 for directories, 666 for files). Example: Default file mode 666 'umask 022' subtracts 022, resulting in 644 (rw-r--r--)

```bash
# User File Creation Mask

umask 022  # Default permissions: rw-r--r-- for files, rwxr-xr-x for directories
umask 077  # Private files and directories: rw-------, rwx------
umask      # Display current umask
```

#### Processes

Foreground Process: Runs in terminal

Background Process: Ends when system reboot or user logs out

```bash
ps              # Display currently running processes.
ps aux          # List all processes
ps -u username  # Show processes of a specific user
pgrep pname     # Find a specific process by name

kill PID        # Terminate processes by ID or name
kill -9 PID     # Force kill

<command> &     # '&' sends to the background

bg              # Resume a stopped process in the background
fg              # Resume a stopped process in the foreground

nice PID        # Affects priority (-20 highest, 19 lowest)
renice -10 PID  # Increase priority
```

#### Shell Scripting

```bash
#!/bin/bash

# Variable & Output
name="Alice"
echo "Hello, $name!"

# Input
read -p "Enter your name: " user
echo "Welcome, $user!"

export MY_VAR="Hello"  # Creates a global variable

# Operators
num=10
if [ $num -gt 5 ]; then
  echo "Number is greater than 5"
else
  echo "Number is 5 or less"
fi

# -eq (equal), -ne (not equal), -gt (greater), -lt (less)
# -f file (file exists), -d dir (directory exists)

# Case
read -p "Enter choice (start/stop): " action
case $action in
  start) echo "Starting..." ;;
  stop) echo "Stopping..." ;;
  *) echo "Invalid option" ;;
esac

# For Loop
for i in {1..5}; do
  echo "Iteration $i"
done

# While Loop
count=1
while [ $count -le 5 ]; do
  echo "Count: $count"
  ((count++))
done

# Always Loop
x=1
until [ $x -gt 3 ]; do
  echo "Value: $x"
  ((x++))
done

# IO Redirection

echo "Hello" > file.txt  # Write to file
echo "More text" >> file.txt  # Append to file
cat < file.txt  # Read from file

# Piping (chain commands by passing output as input)

ls -l | grep "txt"  # Find only .txt files
cat file.txt | sort | uniq  # Sort and remove duplicates

# > → Redirect output (overwrite)
# >> → Append output
# < → Input from file
# 2> → Redirect errors
# &> → Redirect both stdout & stderr

chmod +x script.sh  # Give execute permission
./script.sh  # Run script
```

#### Package Management

1. Debian-based (Ubuntu, Debian)

- apt (Advanced Package Tool)

- dpkg (Debian Package Manager): Install a .deb file:

2. RedHat-based (RHEL, CentOS, Fedora)
   
- yum (Yellowdog Updater, Modified)
- dnf (Modern replacement for yum in Fedora)
- rpm (RedHat Package Manager)

3. Universal

- snap (Canonical's universal package format): Slow in ubuntu
- flatpak (Universal package system for Linux)

#### File Compression

1. tar (Tape Archive) - Combines multiple files into one archive without compression. Often used with gzip for compression.
2. gzip (GNU Zip) - Compresses a single file using the .gz format. Cannot combine multiple files into one (use tar first).
3. gunzip - Used to extract files compressed with gzip.

```bash
tar -czvf archive.tar.gz directory  # Create a compressed archive
tar -xzvf archive.tar.gz -C /path/to/destination # Extract an archive to a specific directory

gzip # Compress files.
gzip file.txt # Compress a file
gzip file1 file2 # Compress multiple files
gzip *.txt # Compress multiple files using wildcards

gunzip *.gz # Decompress multiple files with a wildcard
```

#### File Operations

```bash
find / -mtime -1 # Find files modified within the last 24 hours
find / -user username # Search for files owned by a specific user

lsof # List open files and processes.
lsof /path/to/file # List processes using a specific file
lsof -i # Show network-related processes

tail # Display the last part of a file.
tail file.txt # View the last 10 lines of a file
tail -f log.txt # Continuously display new lines appended to a file

head # Display the beginning of a file.
head -n 15 file.txt # Display a specific number of lines from the start

wc # Display line, word, and character count for a file.
wc -l file.txt # Count lines in a file
wc -w file.txt # Count words in a file

uniq # Report or omit repeated lines in a file.
sort file.txt | uniq # Show unique lines in a sorted file
sort file.txt | uniq -c # Display count of occurrences for unique lines

sort # Sort lines of text files.
sort file.txt # Sort lines in a file
sort -n file.txt # Sort lines numerically

diff # Compare files line by line.
diff file1.txt file2.txt # Compare two files and display differences
diff -r dir1/ dir2/ # Show differences between two directories
```

#### Filesystem Knowledge

| Directory | Purpose |
| - | - |
| /home | Stores user files (e.g., /home/user) |
| /etc | System-wide configuration files (e.g., /etc/passwd) |
| /var | Variable data like logs (/var/log), cache, and temporary files |
| /tmp | Temporary files (auto-cleared on reboot) |
| /usr | User-installed programs (/usr/bin, /usr/lib) |
| /proc | Virtual filesystem with system/process info (/proc/cpuinfo) |

To access an external drive, it must be "mounted" to a directory.

```bash
sudo mount /dev/sdX /mnt
sudo umount /mnt
```

Disk Space Management

```bash
df -h                     # Show available disk space
df -T /dev/sda1           # Display space usage of a specific filesystem
du -sh /path/to/directory # Size of a directory
du -h --max-depth=1 /path # Sizes of all subdirectories
```

#### Networking Basics

```bash
ping example.com    # Check if host is reachable
curl example.com    # Get content of a website
curl -I example.com # Check response headers
curl -X POST -d "data" URL # Send data via POST request

wget https://example.com/file.zip # Download files from the web
wget -O myfile.zip https://example.com/file.zip # Rename

ifconfig    # Display network interface information.
ifconfig -a # List all network interfaces

ss -tulnp # Show open network connections
ss -tnlp  # Check which processes are using ports

traceroute example.com          # Trace the path of network packets
nslookup domain.com # Query DNS servers. Alias: dig

ssh -p 2222 user@remote-server  # Connect to a remote server at port 2222
ssh -i /path/to/private_key user@host # Connect to a server using a specific private key
ssh -L 8080:localhost:80 user@host # Establish an SSH tunnel for port forwarding

scp file.txt user@remote-server:/path/to/destination # Copy a file to a remote server securely
scp -r mydir user@remote-server:/path/to/destination # Copy a directory recursively
scp file.txt user@remote:/path # Copy a file from local to remote

rsync -avz /local/path user@remote-server:/remote/path # Sync a local directory with a remote one
rsync -av --delete /local/path user@remote-server:/remote/path # Delete extra files at the destination

sudo ifconfig eth0 192.168.1.2 netmask 255.255.255.0 # Set an IP address for a specific interface

netstat # Display network connections
netstat -tulnp # Show all listening ports
netstat -s # Display statistics for a specific network protocol

sudo route add -net 192.168.1.0 netmask 255.255.255.0 gw 192.168.0.1 # Add a new route to the routing table
sudo route del -net 192.168.1.0 netmask 255.255.255.0 # Delete a specific route

firewall-cmd/ufw # Configure firewall rules.
sudo ufw allow from 192.168.1.100 # Allow all traffic from a specific IP address
sudo ufw default deny incoming # Deny all incoming traffic by default

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
```

#### Environment Management

Environment variables are added to ~/.bashrc or ~/.profile

```bash
printenv # Print all environment variables
echo 'export MY_VAR="Hello, Linux!"' >> ~/.bashrc # Add environment variable
export MY_VAR="Hello, Linux!" # Temporary add environment variable
source ~/.bashrc              # Reload configuration

echo "alias ll='ls -lah'" >> ~/.bashrc # Make Aliases Permanent
```

| File | Purpose |
| - | - |
| ~/.bashrc | User-specific shell configuration, runs on new interactive shells |
| ~/.profile | User login script, used in login shells |
| /etc/environment | System-wide environment variables |

#### System Performance Monitoring

```bash
top             # Real-time process monitoring
htop            # Real-time process monitoring
vmstat          # Provides information about system performance, including CPU, memory, swap, disk I/O, and system processes
iostat          # Reports CPU usage and disk I/O performance.

tail -n 10 /var/log/syslog  # View Last Few Lines of a Log File
tail -f /var/log/syslog     # Follow log updates in real-time
less /var/log/syslog        # Scroll Through Large Log Files
grep "failed" /var/log/auth.log # Search for Specific Entries in Logs
```

#### Build Tools

gcc is a compiler for C language and g++ is a compiler for C++ language.

`make` (Makefile System) is a build automation tool for unix that compiles complex projects efficiently. `make` only recompiles modified files.

`cmake` is a cross-platform build system generator.

```cmake {title=CMakeLists.txt}
cmake_minimum_required(VERSION 3.10)
project(MyProject)

add_executable(my_program main.cpp utils.cpp)
```

```bash
# Building with CMake
mkdir build && cd build
cmake ..                # Generate Makefiles
make                    # Compile
```

#### Software Development Tools

`venv` (Python Virtual Environment)

```bash
# Create a virtual environment named "myenv"
python -m venv myenv

# Activate on Linux/macOS
source myenv/bin/activate

# Activate on Windows
myenv\Scripts\activate

deactivate
```

`nvm` (Node Version Manager)

```bash
# Check available Node.js versions
nvm ls-remote 

# Install a specific version
nvm install 18

# Switch Node.js version
nvm use 18

# Set a default version
nvm alias default 18
```

`gdb` (GNU Debugger for C/C++)

`strace` (System Call Tracer) is a debugging tool that logs all system calls made by a process.

Tracing a Running Process

#### Users

1. Root User (sudo, root) – The superuser with full system control.
2. Regular User – A non-root user with limited permissions.
3. System Users – Used for system processes (e.g., www-data for web servers).

```bash
hostname # Display or set system hostname.
sudo hostname temporary_name # Change the hostname temporarily

whoami # Display current username.
if [ "$(whoami)" != "root" ]; then echo "Please run as root"; fi

# Create a new group
sudo groupadd groupname

# Add a user to a group
sudo usermod -aG groupname username

# List a user's groups
groups username

# View all groups
cat /etc/group

```

#### System

```bash
name -r   # Check kernel version
uname -m  # Show system architecture
uname -s  # Show only the kernel name

date -u # Display date and time in UTC
date +"%Y-%m-%d %H:%M:%S" # Display date and time in a specific format

uptime # Show how long the system has been running.
uptime # Display system uptime
uptime -p # Show load average for the last 1, 5, and 15 minutes

systemctl # Control system services.
sudo systemctl enable servicename # Enable a service to start at boot
systemctl status ssh # Check the status of a service

journalctl # Query and display system logs.
journalctl -u servicename # Filter logs for a specific service
journalctl --since "2023-12-01 00:00:00" # Display logs since a specific time
```

### Ubuntu 22.04 on VM Windows 11

Shared Folder Location on Host:

C:\MyFolder\Linux_Ubuntu\Ubuntu_SharedFolder
C:\Users\howwi\OneDrive\Coding\UbuntuSF

VM Folder: C:\Users\howwi\VirtualBox VMs\Ubuntu

Shortcuts:

```txt
ctrl + L : Select current directory path in Nautilus(file explorer) to be copied or edit
ctrl + alt + t : Open terminal
ctrl + shift + C : Copy in terminal
ctrl + shift + V : Paste in terminal
ctrl + / : Undo the previous message done in terminal
```

#### Linux Installation (Ubuntu on Windows using Oracle VM)

[Reference](https://ubuntu.com/tutorials/how-to-run-ubuntu-desktop-on-a-virtual-machine-using-virtualbox#1-overview)

1. Download Oracle VM Virtualbox: https://www.virtualbox.org/
2. Download Ubuntu image: https://ubuntu.com/download/desktop
3. Create / Load Machine (guest system): Goto machine -> new machine

| Details | Description |
| --- | --- |
| Name | The name of the environment. If you include the word Ubuntu in your name the Type and Version will auto-update. |
| Machine Folder | This is where your virtual machines will be stored so you can resume working on them whenever you like. |
| ISO Image | Here you need to add a link to the ISO you downloaded from the Ubuntu website. |
| User profile | To secure the ubuntu |
| Add guess addition | Some addition like window sizing support could be added |
| Define the Virtual Machine's resources | Recommended to use at least 8GB RAM, 4 CPUs, 32GB hard disk |
| Create disk | You can create a new disk or load existing disk |

#### Settings

1. Bidirectional "copy and paste" and "drag and drop": Goto VM settings -> general -> advanced, set to bidirectional
2. Enable network: Goto VM settings -> Network -> Adapter1 -> Choose Bridged Adapter1
3. Adding USB: Goto VM settings -> Add new USB -> Choose USB
4. Adding shared folder: Goto VM settings -> Shared Folders -> Set as auto mount and add folder path -> run VM. Make sure guess addition is added, then add user to vboxsf group: { sudo adduser [username] vboxsf } -> restart
5. USB: Download vb extension pack on host [here](https://www.virtualbox.org/wiki/Downloads). Then goto File -> tools -> extension pack manager -> load the extension pack downloaded. Create vboxuser `sudo groupadd vboxusers`. Add yourself into the group `sudo usermod -aG vboxusers your_username`. In VM settings -> USB -> add filter -> start ubuntu -> goto file, then USB is there.
