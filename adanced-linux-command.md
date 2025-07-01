# **Linux System Administration Guide**  
*Mastering File Permissions, User Management, and Advanced Commands*

![Linux Permissions](https://upload.wikimedia.org/wikipedia/commons/thumb/3/3a/Linux_permissions_and_ACLs.svg/1200px-Linux_permissions_and_ACLs.svg.png)

## **Table of Contents**
1. [File Permissions](#-file-permissions)
   - Numeric vs Symbolic Notation
   - `chmod` & `chown`
2. [User Management](#-user-management)
   - Creating Users/Groups
   - Sudo Privileges
3. [Practical Tasks](#-practical-tasks)
4. [Cheat Sheets](#-cheat-sheets)
5. [Resources](#-resources)

---

## **🔐 File Permissions**

### **Permission Notation**
| Symbol | Numeric | Meaning          |
|--------|---------|------------------|
| `r--`  | 4       | Read-only        |
| `rw-`  | 6       | Read + Write     |
| `r-x`  | 5       | Read + Execute   |
| `rwx`  | 7       | Full permissions |

**Example Output:**
```bash
-rwxr-xr-- 1 user group 2048 Jan 1 10:00 script.sh
```
- **`-`**: File type (`d` for directory)  
- **`rwx`**: Owner permissions  
- **`r-x`**: Group permissions  
- **`r--`**: Others permissions  

### **Key Commands**
```bash
# Change permissions (numeric)
chmod 755 file.sh  # rwxr-xr-x

# Change permissions (symbolic)
chmod u+x,g-w,o=r file.sh

# Change ownership
chown user:group file.txt
```

---

## **👥 User Management**

### **User Operations**
```bash
# Create user with home directory
sudo adduser mary

# Grant sudo privileges
sudo usermod -aG sudo mary

# Switch user
su - mary

# Delete user
sudo userdel -r mary  # -r removes home dir
```

### **Group Operations**
```bash
# Create group
sudo groupadd devops

# Add user to group
sudo usermod -aG devops ravi

# Verify groups
id ravi
```

### **Permission Inheritance**
```bash
# Set group ownership
sudo chown :devops /home/dev_projects

# Set SGID for group inheritance
sudo chmod g+s /home/dev_projects
```

---

## **🛠️ Practical Tasks**

### **Task 1: Permission Scenarios**
1. Create a script with:
   ```bash
   touch backup.sh
   chmod 744 backup.sh  # Owner: rwx, Group/Others: r--
   ```
2. Test access as different users

### **Task 2: User/Group Setup**
```bash
# Create devops group and users
sudo groupadd devops
for user in mary mohammed ravi tunji sofia; do
   sudo adduser $user
   sudo usermod -aG devops $user
   sudo mkdir /home/$user/projects
   sudo chown $user:devops /home/$user/projects
done
```

### **Task 3: Sudo Practice**
```bash
# Allow devops group to run apt commands
echo "%devops ALL=(ALL) /usr/bin/apt" | sudo tee /etc/sudoers.d/devops
```

---

## **📜 Cheat Sheets**

### **Permission Quick Reference**
| Command | Effect |
|---------|--------|
| `chmod 777` | Full access for all |
| `chmod 600` | Owner: rw-, Others: none |
| `chmod +x`  | Add execute permission |

### **User Management**
| Command | Description |
|---------|-------------|
| `passwd user` | Change password |
| `groups user` | Show user groups |
| `visudo` | Edit sudoers file safely |

---

### Screenshot

<img width="615" alt="Snipaste_2025-07-01_11-19-11" src="https://github.com/user-attachments/assets/6dc7a1ee-5dbe-4843-acfb-ab5b0564e31b" />


<img width="437" alt="Snipaste_2025-07-01_11-20-58" src="https://github.com/user-attachments/assets/7c3bc530-e618-42e1-aad4-65845a74feaa" />


<img width="458" alt="Snipaste_2025-07-01_11-22-50" src="https://github.com/user-attachments/assets/210cd509-356f-40a6-a296-29a81cc4f56f" />


<img width="444" alt="Snipaste_2025-07-01_11-25-27" src="https://github.com/user-attachments/assets/b94771b6-a54c-4b0f-ad45-091936ee0065" />


## **📚 Resources**
- [Linux Permissions Explained](https://linuxhandbook.com/linux-file-permissions/)
- [User Management Guide](https://ubuntu.com/server/docs/security-users)
- [Sudoers File Syntax](https://www.sudo.ws/docs/man/1.8.15/sudoers.man/)

```bash
# Quick Check
echo "System Administration Skills: ✅" | sudo tee /var/log/training.log
```

---

**Pro Tip**: Always use `visudo` instead of directly editing `/etc/sudoers` to avoid syntax errors!  
*"With great sudo power comes great responsibility."* - Linux Admin Proverb
