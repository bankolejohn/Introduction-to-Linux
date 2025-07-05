# **Bash Scripting: Control Flow & Loops**  
*A comprehensive guide to conditional statements and looping constructs in Bash*

![Bash Control Flow](https://upload.wikimedia.org/wikipedia/commons/thumb/8/8f/Bash_screenshot.png/800px-Bash_screenshot.png)

## **Table of Contents**
1. [Number Classification Script](#-number-classification-script)
2. [Understanding Control Flow](#-understanding-control-flow)
3. [Looping Constructs](#-looping-constructs)
   - For Loops
   - While Loops
   - Until Loops
4. [Practical Tasks](#-practical-tasks)
5. [Cheat Sheets](#-cheat-sheets)

---

## **🔢 Number Classification Script**

### **Complete Script**
```bash
#!/bin/bash

read -p "Enter a number: " num

if [ $num -gt 0 ]; then
    echo "The number is positive."
elif [ $num -lt 0 ]; then
    echo "The number is negative."
else
    echo "The number is zero."
fi
```

### **How to Use**
1. Save as `number_classifier.sh`
2. Make executable: 
   ```bash
   chmod +x number_classifier.sh
   ```
3. Run:
   ```bash
   ./number_classifier.sh
   ```

---

## **⚙️ Understanding Control Flow**

### **Key Components**
| Component | Purpose | Example |
|-----------|---------|---------|
| `if` | Starts conditional block | `if [ $age -ge 18 ]` |
| `elif` | Alternative condition | `elif [ $age -lt 13 ]` |
| `else` | Default case | `else echo "Teenager"` |
| `fi` | Ends conditional block | |

### **Comparison Operators**
| Operator | Meaning | Numeric | String |
|----------|---------|---------|--------|
| `-gt` | Greater than | `[ $a -gt $b ]` | |
| `-lt` | Less than | `[ $a -lt $b ]` | |
| `-eq` | Equal | `[ $a -eq $b ]` | `[ "$str1" = "$str2" ]` |
| `-ne` | Not equal | `[ $a -ne $b ]` | `[ "$str1" != "$str2" ]` |

---

## **🔄 Looping Constructs**

### **1. For Loops**
**List Form:**
```bash
for fruit in apple banana cherry; do
    echo "I like $fruit"
done
```

**Range Form:**
```bash
for i in {1..5}; do
    echo "Count: $i"
done
```

**C-style Form:**
```bash
for (( i=0; i<5; i++ )); do
    echo "Iteration $i"
done
```

### **2. While Loops**
```bash
counter=1
while [ $counter -le 5 ]; do
    echo "Counter: $counter"
    ((counter++))
done
```

### **3. Until Loops**
```bash
countdown=5
until [ $countdown -eq 0 ]; do
    echo "$countdown..."
    sleep 1
    ((countdown--))
done
echo "Liftoff!"
```

---

## **🛠️ Practical Tasks**

### **Task 1: Enhanced Number Classifier**
```bash
#!/bin/bash
read -p "Enter a number: " num

if ! [[ "$num" =~ ^-?[0-9]+$ ]]; then
    echo "Error: Not a valid number" >&2
    exit 1
elif [ $num -gt 0 ]; then
    echo "Positive number"
elif [ $num -lt 0 ]; then
    echo "Negative number"
else
    echo "Zero"
fi
```

### **Task 2: Directory Processor**
```bash
#!/bin/bash
for file in /var/log/*.log; do
    echo "Processing $file"
    wc -l < "$file"
done
```

### **Task 3: User Input Validation**
```bash
#!/bin/bash
while true; do
    read -p "Enter password (min 8 chars): " pw
    if [ ${#pw} -ge 8 ]; then
        echo "Password accepted!"
        break
    else
        echo "Too short, try again"
    fi
done
```

---

## **📜 Cheat Sheets**

### **Loop Control**
| Command | Effect |
|---------|--------|
| `break` | Exit loop immediately |
| `continue` | Skip to next iteration |
| `exit` | Terminate entire script |

### **Special Variables**
| Variable | Purpose |
|----------|---------|
| `$1`, `$2` | Positional arguments |
| `$#` | Argument count |
| `$?` | Exit status of last command |

---

## **📚 Resources**
- [Bash Conditional Expressions](https://www.gnu.org/software/bash/manual/html_node/Conditional-Constructs.html)
- [Looping in Bash](https://linuxize.com/post/bash-for-loop/)
- [Advanced Bash-Scripting Guide](https://tldp.org/LDP/abs/html/)

```bash
# Quick Test: Count loop types in your scripts
grep -c -E 'for|while|until' *.sh
```

---

**Pro Tip**: Use `set -x` at script start to debug loops:
```bash
#!/bin/bash
set -x  # Debug mode
for i in {1..3}; do
    echo "Debugging iteration $i"
done
```

*"Good scripts flow like rivers - with purpose and without unnecessary turns."* - Ancient DevOps Proverb
