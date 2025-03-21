### **Basics of Shell Scripting**

Shell scripting is a way to automate tasks in Unix/Linux systems by writing a series of commands in a script file. A shell script is executed by a shell, such as **Bash (Bourne Again Shell), Zsh, KornShell (ksh), or Dash**.

## **1. Writing Your First Shell Script**
### **Steps to Create and Execute a Shell Script**
1. **Create a script file:**  
   ```sh
   nano myscript.sh
   ```
2. **Add the shebang (`#!`) at the top:**  
   ```sh
   #!/bin/bash
   echo "Hello, World!"
   ```
3. **Save and exit (Ctrl + X → Y → Enter).**
4. **Give execute permission:**  
   ```sh
   chmod +x myscript.sh
   ```
5. **Run the script:**  
   ```sh
   ./myscript.sh
   ```

---

## **2. Shell Script Basics**
### **Shebang (`#!`)**
The first line of a script tells the system which interpreter to use.
- **Bash:** `#!/bin/bash`
- **Sh:** `#!/bin/sh`
- **Python (if needed):** `#!/usr/bin/python3`

### **Variables**
Define and use variables without spaces:
```sh
name="Alice"
echo "Hello, $name"
```

### **User Input**
```sh
echo "Enter your name:"
read user_name
echo "Welcome, $user_name!"
```

### **Comments**
- **Single-line:** `# This is a comment`
- **Multi-line:**  
  ```sh
  : '
  This is a
  multi-line comment
  '
  ```

---

## **3. Control Structures**
### **Conditional Statements**
```sh
#!/bin/bash
echo "Enter a number:"
read num

if [ $num -gt 10 ]; then
    echo "Number is greater than 10"
else
    echo "Number is 10 or less"
fi
```
- `[ condition ]` or `[[ condition ]]` is used for conditions.
- Operators:  
  - `-eq` (equal), `-ne` (not equal)
  - `-lt` (less than), `-gt` (greater than)
  - `-le` (less than or equal), `-ge` (greater than or equal)

### **Loops**
#### **For Loop**
```sh
for i in 1 2 3 4 5
do
  echo "Iteration: $i"
done
```

#### **While Loop**
```sh
count=1
while [ $count -le 5 ]
do
  echo "Count: $count"
  count=$((count + 1))
done
```

---

## **4. Functions**
Functions help in code reuse.
```sh
greet() {
  echo "Hello, $1!"
}

greet "Alice"
```
- `$1` represents the first argument passed.

---

## **5. File Handling**
### **Check If a File Exists**
```sh
if [ -f "file.txt" ]; then
  echo "File exists"
else
  echo "File does not exist"
fi
```

### **Read a File Line by Line**
```sh
while read line; do
  echo "Line: $line"
done < file.txt
```

---

## **6. Special Variables**
| Variable | Description |
|----------|-------------|
| `$0` | Script name |
| `$1, $2, ...` | Positional arguments |
| `$#` | Number of arguments |
| `$@` | All arguments |
| `$$` | Process ID of the script |
| `$?` | Exit status of the last command |

Example:
```sh
echo "Script Name: $0"
echo "First Argument: $1"
echo "Number of Arguments: $#"
```

---

## **7. Exit Status**
Every command returns an exit status:
- `0` → Success
- `Non-zero` → Error

Check the exit status:
```sh
mkdir test_directory
if [ $? -eq 0 ]; then
  echo "Directory created successfully"
else
  echo "Failed to create directory"
fi
```

---

## **8. Scheduling Scripts**
### **Using `cron` for Automation**
Edit the cron jobs:
```sh
crontab -e
```
Example cron job to run a script every day at 8 AM:
```
0 8 * * * /path/to/myscript.sh
```

---

## **9. Debugging Shell Scripts**
Use `-x` to debug:
```sh
bash -x myscript.sh
```
Or add `set -x` inside the script.

---

## **10. Advanced Topics**
- **Piping and Redirection**
  ```sh
  ls -l | grep "myfile"
  echo "Hello" > file.txt  # Overwrite
  echo "World" >> file.txt  # Append
  ```
- **Process Management**
  ```sh
  ps aux | grep "bash"
  kill -9 <PID>
  ```
- **Background Jobs**
  ```sh
  ./script.sh &
  ```

---

## **Conclusion**
Shell scripting is powerful for automating tasks, managing files, and handling system operations. Mastering it will help you efficiently manage servers, automate processes, and execute commands efficiently.

