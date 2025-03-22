# Shell Scripting

Shell scripting is writing a series of commands in a text file to be executed by a Unix/Linux shell (like Bash, Zsh, or Sh). Instead of typing commands one by one, you can automate tasks by running the script.

## Why it’s used:

- **Automation:** Repetitive tasks (e.g., backups, file management, deployments).
- **Task scheduling:** Combined with tools like cron for recurring jobs.
- **System administration:** Managing servers, installing packages, and configuring environments.
- **Batch processing:** Running multiple commands or programs sequentially or conditionally.
- **Scripting pipelines:** Connecting commands and processing text with utilities like `grep`, `awk`, and `sed`.

## Shebang
The shebang (`#!`) at the beginning of a script specifies the interpreter to be used to execute the script.
For example:
- `#!/bin/bash` - Uses the Bash shell.
- `#!/bin/sh` - Uses the system's default shell, which could be `sh`, `dash`, or another shell depending on the OS.

## Sudo and Su
- **sudo:** Allows a permitted user to execute a command as the superuser or another user, as specified by the security policy.
- **su:** Switches to another user, typically the superuser, by prompting for the target user's password.

### Common sudo/su commands:
1. **Switch to Root User (Login as Root)**: `sudo -i` or `sudo su`
2. **Run a Single Command as Root**: `sudo command`
3. **Switch to the Root User Directly**: `su -`
4. **Check If I have Sudo Access**: `sudo -l`
5. **Add myself to the sudo Group**: `usermod -aG sudo manjunath_dc`

## Shell Differences
- **Bash:** Bourne Again SHell, feature-rich.
- **Dash:** Debian Almquist SHell, lighter and faster.
- **Sh:** Bourne SHell, the original Unix shell.
- **Ksh:** Korn SHell, combines features of sh and bash.

## Variables and Input

### Example 1: Declare Variables
```bash
name="John"
echo "Hello, $name!"
```

### Example 2: Read User Input
```bash
echo "Enter your name:"
read name
echo "Hello, $name!"
```

### Example 3: Command-line Arguments
```bash
echo "First argument: $1"
echo "All arguments: $@"
echo "Total arguments: $#"
```

## Safety Measures for Using sudo in DevOps:
1. **Least Privilege:** Grant only the necessary permissions.
2. **Audit Logs:** Keep logs of sudo usage.
3. **Time-bound Access:** Use sudo with time-bound permissions.
4. **Secure Configuration:** Ensure `/etc/sudoers` is securely configured.

## Linking in Linux
- **Soft Link (Symbolic Link):** Points to another file by name. Can span filesystems.
- **Hard Link:** Points directly to the inode of the file. Cannot span filesystems.

## Chmod
`chmod` changes file permissions. Permissions are divided into three categories:
- **User (Owner)**
- **Group**
- **Others**

### Permission Representation:
- `4`: Read
- `2`: Write
- `1`: Execute

Example:
```bash
chmod 755 filename
```
This gives read, write, execute to the owner, and read and execute to the group and others.

## Basic Commands
- `pwd`: Print current working directory.
- `mkdir`: Create a directory.
- `ls -ltr`: List files in long format, sorted by modification time (reverse).
- `cd`: Change directory.
- `mv`: Move or rename files.
- `cp`: Copy files.
- `touch`: Create an empty file or update the timestamp.

## Role of Shell Scripting in DevOps
1. **Infra Maintenance:** Automate routine tasks.
2. **Git Interaction:** Automate Git operations.
3. **Configuration Management:** Automate configuration tasks.

## Commands for System Health
- `nproc`: Number of processing units available.
- `free`: Display memory usage.
- `top`: Display system processes.

### Example Script to Check Node Health:
```bash
#!/bin/bash
set -exo pipefail
echo "CPU Cores: $(nproc)"
echo "Memory Usage:"
free -h
echo "Top Processes:"
top -b -n 1 | head -n 20
```

## Debugging
- `set -x`: Enables debug mode, printing each command before execution.

### Example:
```bash
#!/bin/bash
set -x
echo "Debug mode is on"
```

## Process Management
- `ps -ef`: Lists all processes. Use `grep` to filter.

### Example:
```bash
ps -ef | grep "amazon"
```
To fetch the process ID:
```bash
ps -ef | grep "amazon" | awk '{print $2}'
```

## Date and Echo
Use command substitution:
```bash
echo "Today is $(date)"
```

## Awk Command
Processes text.
```bash
ps -ef | grep amazon | awk '{print $2}'
```

## Set -e and Set -o Pipefail
- `set -e`: Exit on error.
- `set -o pipefail`: Exit on error in a pipeline.

### Example:
```bash
#!/bin/bash
set -exo pipefail
false | true
echo "This will not be printed"
```

## Curl vs Wget
- **curl:** Supports more protocols, outputs to stdout.
- **wget:** Supports recursive downloading, outputs to file.

## Find Command
Find files by name:
```bash
find /path/to/search -name "filename"
```

## If-Else and Loops
### If-Else Example:
```bash
if [ "$1" == "hello" ]; then
    echo "Hello World"
else
    echo "Goodbye"
fi
```

### For Loop Example:
```bash
for i in {1..5}; do
    echo "Number: $i"
done
```

### While Loop Example:
```bash
count=1
while [ $count -le 5 ]; do
    echo "Count: $count"
    count=$((count + 1))
done
```

### Until Loop Example:
```bash
count=1
until [ $count -gt 5 ]; do
    echo "Count: $count"
    count=$((count + 1))
done
```

## Signals in Linux
Common signals:
1. `SIGINT`: Interrupt (Ctrl+C)
2. `SIGTERM`: Termination
3. `SIGKILL`: Kill
4. `SIGHUP`: Hangup
5. `SIGSTOP`: Stop

### Trap Example:
```bash
trap "rm -rf *" SIGINT
```
This script will delete all files in the current directory if interrupted.

