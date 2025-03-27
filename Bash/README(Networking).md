# Linux File System Navigation & Networking Commands

## File System Navigation
The Linux file system is hierarchical, with directories and files structured in a tree format. Understanding how to navigate and manipulate files is essential.

### Common Commands

| Command  | Description |
|----------|------------|
| `cd`     | Change directory |
| `ls`     | List files and directories |
| `pwd`    | Print current working directory |
| `mkdir`  | Create a new directory |
| `rm`     | Remove files or directories |
| `cp`     | Copy files and directories |
| `mv`     | Move or rename files and directories |
| `touch`  | Create an empty file or update its timestamp |
| `find`   | Search for files and directories based on criteria |
| `locate` | Quickly find files using a pre-indexed database |

### Paths
- **Absolute Path**: Starts from the root (`/`).  
  _Example_: `/home/user/Documents`
- **Relative Path**: Based on the current directory.  
  _Example_: `../Documents`

---

## Networking Commands
Networking commands help in troubleshooting and monitoring network activities.

### Common Commands

| Command  | Description |
|----------|------------|
| `ping`   | Checks connectivity to a remote host |
| `curl`   | Transfers data from or to a server |
| `wget`   | Downloads files from the internet |
| `ssh`    | Securely connects to a remote machine |
| `scp`    | Securely copies files between computers |
| `netstat` | Displays network connections |
| `ifconfig` | Shows or configures network interfaces (deprecated) |
| `ip` | Replaces `ifconfig` to manage IP addresses |
| `nslookup` | Queries DNS servers |
| `dig` | Performs DNS lookups |

### Command Usage Scenarios

#### 1. `ping` - Check Network Connectivity
**Scenario**: Verify connectivity between instances

```sh
# Ping Instance B from Instance A using the private IP (same VPC)
ping 192.168.1.20 -c 4

# Ping Instance B from a local machine using the public IP
ping Y.Y.Y.Y -c 4
```

**Expected Outcome**:
- If successful, network connectivity exists.
- If the ping fails, check if ICMP is allowed in the Security Group.

---

#### 2. `curl` - Fetch Data from a Remote Server
**Scenario**: Test a web service running on an EC2 instance

```sh
# Start a simple web server on Instance A
sudo yum install -y httpd
sudo systemctl start httpd
sudo systemctl enable httpd

# Fetch the web page from Instance B
curl http://192.168.1.10

# Fetch the same web page from your local machine
curl http://X.X.X.X
```

**Expected Outcome**:
- If successful, the HTML content of the web page is displayed.
- If the request times out, check the Security Group for inbound rules on port 80.

---

#### 3. `wget` - Download a File from the Internet
**Scenario**: Download a software package on an EC2 instance

```sh
# Download a file from the internet on Instance A
wget https://example.com/sample-file.zip

# Download a file from Instance A to Instance B using the public IP
wget http://X.X.X.X/sample-file.zip
```

**Expected Outcome**:
- If successful, the file is saved locally.
- If failed, check outbound rules for HTTP access.

---

#### 4. `ssh` - Securely Connect to Another EC2 Instance
**Scenario**: Connect from your local machine to an EC2 instance

```sh
# From your local machine, SSH into Instance A
ssh -i my-key.pem ec2-user@X.X.X.X

# From Instance A, SSH into Instance B using its private IP
ssh ec2-user@192.168.1.20
```

**Expected Outcome**:
- If successful, the user logs into the remote instance.
- If failed, check that SSH (port 22) is allowed in the Security Group.

---

#### 5. `scp` - Securely Copy Files Between EC2 Instances
**Scenario**: Transfer a file from Instance A to Instance B

```sh
# Create a file on Instance A
echo "Hello from Instance A" > test.txt

# Copy the file from Instance A to Instance B using the private IP
scp -i my-key.pem test.txt ec2-user@192.168.1.20:/home/ec2-user/

# Verify on Instance B
ls -l /home/ec2-user/test.txt
```

**Expected Outcome**:
- If successful, `test.txt` appears on Instance B.
- If failed, check that SSH is allowed.

---

#### 6. `netstat` - Display Active Network Connections
**Scenario**: Check if an EC2 instance is listening on a specific port

```sh
# Check open ports on Instance A
sudo netstat -tulnp

# Filter for a specific service, e.g., SSH
sudo netstat -tulnp | grep ssh
```

**Expected Outcome**:
- If successful, active network connections are listed.
- If a service isn't running, check if it is enabled.

---

#### 7. `ifconfig` (Deprecated) & `ip` - Check Network Configuration
**Scenario**: View and manage network interfaces on an EC2 instance

```sh
# Check network interfaces using ifconfig
ifconfig

# Check network interfaces using ip
ip addr show

# Display routing table
ip route show
```

**Expected Outcome**:
- Lists private and public IP addresses, network interfaces, and routes.

---

#### 8. `nslookup` - Query DNS Information
**Scenario**: Resolve domain names from an EC2 instance

```sh
# Check the IP address of Google
nslookup google.com

# Check the IP address of your EC2 instance hostname
nslookup X.X.X.X
```

**Expected Outcome**:
- Displays DNS resolution results.

---

#### 9. `dig` - Perform Advanced DNS Lookups
**Scenario**: Perform detailed DNS queries from an EC2 instance

```sh
# Get detailed DNS information for Google
dig google.com

# Check the mail server (MX record) of a domain
dig google.com MX

# Check the authoritative nameservers of a domain
dig google.com NS
```

**Expected Outcome**:
- Displays DNS resolution details.

---

## Conclusion

These Linux commands are essential for file system navigation and networking. Understanding their usage will help in managing servers, troubleshooting issues, and performing administrative tasks efficiently.
