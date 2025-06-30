# **Linux Text Editors Guide**  
*A comprehensive handbook for Vim and Nano text editors in Linux environments*

![Linux Text Editors](https://upload.wikimedia.org/wikipedia/commons/thumb/9/9f/Vimlogo.svg/1200px-Vimlogo.svg.png)

## **Table of Contents**
1. [Introduction to Linux Text Editors](#-introduction-to-linux-text-editors)  
2. [Vim Text Editor](#%EF%B8%8F-vim-text-editor)  
   - Basic Operations  
   - Navigation & Editing  
   - Saving & Exiting  
3. [Nano Text Editor](#-nano-text-editor)  
   - Basic Operations  
   - Keyboard Shortcuts  
4. [Cheat Sheet Comparison](#-cheat-sheet-comparison)  
5. [Practice Exercises](#-practice-exercises)  

---

## **📝 Introduction to Linux Text Editors**
Linux text editors are essential tools for:
- Editing configuration files (`/etc/`, `.config`)  
- Writing scripts (Bash, Python)  
- Creating documentation (Markdown, plain text)  

**Popular Options**:
- **Vim**: Powerful, modal editor (steep learning curve)  
- **Nano**: Beginner-friendly, simple interface  
- Others: Emacs, VS Code (with SSH extension)  

---

## **✍️ Vim Text Editor**
### **1. Launching Vim**
```bash
vim exercise.txt  # Creates/opens file
```

### **2. Modes**
| Mode | Key | Purpose |
|------|-----|---------|
| **Normal** | `Esc` | Navigation/deletion |
| **Insert** | `i` | Text input |
| **Visual** | `v` | Text selection |

### **3. Essential Commands**
| Task | Command |
|------|---------|
| Save | `:w` |
| Save & Quit | `:wq` |
| Quit (no save) | `:q!` |
| Delete line | `dd` |
| Undo | `u` |
| Search | `/keyword` |

### **4. Navigation (Normal Mode)**
```text
h ←   j ↓   k ↑   l →
```

---

## **🖱️ Nano Text Editor**
### **1. Launching Nano**
```bash
nano nano_file.txt  # Creates/opens file
```

### **2. Keyboard Shortcuts**
| Shortcut | Action |
|----------|--------|
| `Ctrl+O` | Save |
| `Ctrl+X` | Exit |
| `Ctrl+K` | Cut line |
| `Ctrl+U` | Paste |
| `Ctrl+W` | Search |
| `Ctrl+\` | Replace |

### **3. Basic Workflow**
1. Type text directly (no mode switching)
2. Save with `Ctrl+O` → Confirm filename
3. Exit with `Ctrl+X` (prompts to save if unsaved)

---

## **📜 Cheat Sheet Comparison**
| Feature | Vim | Nano |
|---------|-----|------|
| **Learning Curve** | Steep | Easy |
| **Modes** | Multiple (Normal/Insert/Visual) | Single |
| **File Save** | `:w` | `Ctrl+O` |
| **Exit** | `:q` | `Ctrl+X` |
| **Search** | `/text` | `Ctrl+W` |
| **Best For** | Advanced users, scripting | Beginners, quick edits |

---

## **💻 Practice Exercises**
### **Vim Challenges**
1. Create `script.sh` and add:
   ```bash
   #!/bin/bash
   echo "Hello from Vim!"
   ```
   - Save with `:wq`

2. Practice navigation:
   - Move to line start/end (`0` / `$`)
   - Jump between words (`w` / `b`)

### **Nano Challenges**
1. Edit `/etc/hosts` (requires `sudo`):
   ```bash
   sudo nano /etc/hosts
   ```
   - Add: `127.0.0.1  mytest.site`

2. Use search (`Ctrl+W`) to find "localhost"

---

## **🚀 Pro Tips**
- **Vim**:  
  - Enable line numbers: `:set number`  
  - Repeat last action: `.`  

- **Nano**:  
  - Enable smooth scrolling: `nano -S file.txt`  
  - View help: `Ctrl+G`  

---

## Screenshots

<img width="189" alt="Snipaste_2025-06-30_11-15-39" src="https://github.com/user-attachments/assets/4e65bf26-c051-4d93-8ff5-8db25167de40" />


<img width="549" alt="Snipaste_2025-06-30_11-16-26" src="https://github.com/user-attachments/assets/3f5523e1-6b27-49f7-b0e7-a8d11cb6bf94" />


<img width="960" alt="Snipaste_2025-06-30_11-17-46" src="https://github.com/user-attachments/assets/7b5d2464-cda3-4c1c-ab77-856dc3eff4d0" />

<img width="597" alt="Snipaste_2025-06-30_11-18-47" src="https://github.com/user-attachments/assets/2ee7de7d-bd54-440f-ab0e-a552cda177a2" />


## **📚 Resources**
- [Vim Interactive Tutorial](https://www.openvim.com/)  
- [Nano Official Docs](https://www.nano-editor.org/docs.php)  
- [Vim Cheat Sheet](https://vim.rtorr.com/)  

```bash
# Quick Test (Run in Terminal)
echo "Mastered Linux editors? 🎯" | vim -  
```
