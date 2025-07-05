# **Linux Shell Scripting Project Guide**  
*Creating, Permissions, and Executing Your First Bash Script*

![Bash Scripting](https://upload.wikimedia.org/wikipedia/commons/thumb/4/4b/Bash_Logo_Colored.svg/1200px-Bash_Logo_Colored.svg.png)

## **Table of Contents**
1. [Project Setup](#-project-setup)
2. [Script Creation with Vim](#-script-creation-with-vim)
3. [Understanding Permissions](#-understanding-permissions)
4. [Executing the Script](#-executing-the-script)
5. [Shebang Explained](#-shebang-explained)
6. [Variables in Bash](#-variables-in-bash)
7. [Verification Tasks](#-verification-tasks)

---

## **📂 Project Setup**

### **1. Create Project Directory**
```bash
mkdir ~/shell-scripting
cd ~/shell-scripting
```

### **2. Verify Directory Creation**
```bash
pwd  # Should show: /home/your_user/shell-scripting
```

---

## **✍️ Script Creation with Vim**

### **1. Create Script File**
```bash
vim my_first_shell_script.sh
```

### **2. Insert This Code (Press `i` to enter Insert Mode)**
```bash
#!/bin/bash

# Create directories
mkdir dir1 dir2 dir3

# Create users
sudo useradd user1
sudo useradd user2
sudo useradd user3

echo "Script executed successfully!"
```

### **3. Save & Exit Vim**
1. Press `Esc` to exit Insert Mode  
2. Type `:wq` and press `Enter`

### **4. Verify File Creation**
```bash
ls -latr
```
**Expected Output:**
```
total 12
-rw-r--r-- 1 user user  149 Feb 11 14:35 my_first_shell_script.sh
drwxr-xr-x 1 user user 4096 Feb 11 14:36 ..
drwxr-xr-x 2 user user 4096 Feb 11 14:36 .
```

---

## **🔐 Understanding Permissions**

### **Current Permissions**
```bash
-rw-r--r-- 
```
- **Owner**: Read + Write  
- **Group/Others**: Read Only  
- **No Execute Permissions** for anyone

### **Add Execute Permission**
```bash
chmod u+x my_first_shell_script.sh
```
**Updated Permissions:**
```bash
-rwxr--r--  # Owner can now execute
```

---

## **🚀 Executing the Script**

### **Run the Script**
```bash
./my_first_shell_script.sh
```

### **Expected Output**
```
Script executed successfully!
```

### **Verify Results**
```bash
# Check directories
ls -d dir*/  

# Check users
id user1
id user2 
id user3
```

---

## **#! Shebang Explained**

### **Purpose**
- Specifies the interpreter path (`/bin/bash`)  
- Required for direct execution (`./script.sh`)

### **Common Shebangs**
| Shebang | Use Case |
|---------|----------|
| `#!/bin/bash` | Standard Bash scripts | 
| `#!/bin/sh` | POSIX-compliant scripts |
| `#!/usr/bin/python3` | Python scripts |

### **View Available Shells**
```bash
ls /bin/*sh
```

---

## **📦 Variables in Bash**

### **Variable Declaration**
```bash
name="John"
age=30
files=$(ls)  # Command substitution
```

### **Usage Examples**
```bash
echo $name          # Output: John
echo "Age: $age"    # Output: Age: 30
echo "Files: $files" # Lists directory contents
```

### **Best Practices**
- **Uppercase** for constants (`MAX_USERS=100`)  
- **Lowercase** for local variables  
- **Quote variables** to prevent globbing: `"$name"`

---

## **✅ Verification Tasks**

### **Task 1: Permission Update**
```bash
chmod 744 my_first_shell_script.sh  # rwxr--r--
```

### **Task 2: Script Enhancement**
Add this to your script:
```bash
# Variable example
admin="SysAdmin"
echo "Welcome, $admin!"
```

### **Task 3: Cleanup (Optional)**
```bash
# Remove created directories/users
rm -rf dir1 dir2 dir3
sudo userdel user1 user2 user3
```

---

## Screenshots

<img width="572" alt="Snipaste_2025-07-05_02-58-12" src="https://github.com/user-attachments/assets/82957e13-b3c6-4d13-a2fe-561ba162160a" />


<img width="549" alt="Snipaste_2025-07-05_03-08-12" src="https://github.com/user-attachments/assets/7c41d614-e711-4d74-8162-1d39d3be0037" />


<img width="494" alt="Snipaste_2025-07-05_03-10-27" src="https://github.com/user-attachments/assets/6d0a8239-1e33-452b-b74c-3d56e80b890a" />


## **📚 Resources**
- [Bash Scripting Tutorial](https://linuxconfig.org/bash-scripting-tutorial)
- [File Permissions Guide](https://linuxhandbook.com/linux-file-permissions/)
- [Vim Cheat Sheet](https://vim.rtorr.com/)

```bash
# Final Check
[ -x "my_first_shell_script.sh" ] && echo "Ready to execute!" || echo "Check permissions"
```

---

**Pro Tip**: Always test scripts in a safe environment before running them with `sudo`!  
*"Good scripts make happy sysadmins."* - Ancient Linux Proverb
