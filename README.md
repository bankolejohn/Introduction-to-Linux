# Introduction-to-Linux

Here's a comprehensive **README.md** for your Linux Introduction project, formatted for GitHub with clear macOS-specific setup instructions:

```markdown
# Introduction to Linux - macOS Setup Guide

![Linux Logo](https://upload.wikimedia.org/wikipedia/commons/thumb/3/35/Tux.svg/1200px-Tux.svg.png)

## 🐧 Project Overview
This project provides a hands-on introduction to Linux fundamentals, focusing on:
- Setting up a cloud-based Linux server (Ubuntu on AWS EC2)
- Connecting via SSH from macOS
- Basic package management (APT)
- Essential Linux commands

## 🖥️ macOS Setup Guide

### 1. AWS EC2 Instance Setup
1. **Create AWS Account**  
   [Register for AWS Free Tier](https://aws.amazon.com/free)

2. **Launch Ubuntu Server**  
   - Navigate to EC2 Dashboard
   - Click "Launch Instance"
   - Select "Ubuntu Server 22.04 LTS"
   - Choose `t2.micro` (Free Tier eligible)
   - Download new key pair (`ubuntu.pem`)

### 2. macOS Terminal Setup
```bash
# No additional tools needed - macOS has built-in SSH client
# Open Terminal from:
# Applications → Utilities → Terminal
```

### 3. Connecting to EC2 Instance
1. **Secure your key file**:
```bash
chmod 400 ~/Downloads/ubuntu.pem
```

2. **SSH Connection**:
```bash
ssh -i "~/Downloads/ubuntu.pem" ubuntu@YOUR_PUBLIC_IP
```
![SSH Connection](https://miro.medium.com/v2/resize:fit:1400/1*Q6a6ExFU8WtT0jZqCdjlFw.png)

## 🛠️ Linux Fundamentals

### Package Management (APT)
| Command | Description |
|---------|-------------|
| `sudo apt update` | Refresh package lists |
| `sudo apt install tree` | Install software |
| `sudo apt upgrade` | Update installed packages |
| `sudo apt remove tree` | Remove software |

### File System Navigation
```bash
tree ~/Downloads       # View directory structure
ls -l                  # List files with details
cd /var/www            # Change directory
pwd                    # Show current directory
```

## 🧩 Practice Exercises
1. Install Nginx web server:
```bash
sudo apt install nginx
```

2. Verify installation:
```bash
systemctl status nginx
```

3. Create a test file:
```bash
echo "Hello Linux!" > test.txt
```

## 📚 Learning Resources
- [Linux Command Cheat Sheet](https://ubuntu.com/tutorials/command-line-for-beginners)
- [SSH Essentials](https://www.ssh.com/academy/ssh)
- [AWS EC2 Documentation](https://docs.aws.amazon.com/ec2/)

## 🚀 Next Steps
1. Configure Nginx to host a simple webpage
2. Set up user permissions
3. Automate tasks with bash scripting

---
**Note**: Always terminate your EC2 instance after practice to avoid charges!
```bash
# Disconnect from SSH
exit
```

[![AWS](https://img.shields.io/badge/AWS-EC2-orange)](https://aws.amazon.com/ec2/)
[![macOS](https://img.shields.io/badge/macOS-Terminal-blue)](https://support.apple.com/guide/terminal/welcome/mac)
```

### Key Features:
1. **macOS-Specific Instructions**  
   - Leverages built-in Terminal/SSH
   - Proper PEM key permissions setup

2. **Visual Aids**  
   - Badges for AWS/macOS
   - Command syntax highlighting

3. **Structured Learning Path**  
   - Setup → Fundamentals → Practice → Next Steps

4. **Safety Reminders**  
   - EC2 termination warning
   - Key file security (`chmod 400`)

5. **Quick-Reference Tables**  
   - APT commands
   - Basic file operations

This README provides a complete onboarding experience for macOS users while maintaining relevance for all learners. The markdown formatting ensures proper rendering on GitHub.

## Screenshots

<img width="983" alt="Snipaste_2025-06-30_08-44-25" src="https://github.com/user-attachments/assets/b576327f-13a2-4e83-9c5d-0a177570b03f" />


<img width="850" alt="Snipaste_2025-06-30_08-50-49" src="https://github.com/user-attachments/assets/eeeeee6f-fcf1-4660-a806-010dbf11cb2b" />


<img width="1384" alt="Snipaste_2025-06-30_08-53-11" src="https://github.com/user-attachments/assets/b844e8e9-8b63-47f4-860a-9dcebae105e7" />
