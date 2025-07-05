# **Bash Multiplication Table Generator**

![Multiplication Table](https://upload.wikimedia.org/wikipedia/commons/thumb/e/eb/Multiplication_table_%2810x10%29.jpg/800px-Multiplication_table_%2810x10%29.jpg)

## **Table of Contents**
1. [Project Overview](#-project-overview)
2. [Script Features](#-script-features)
3. [Usage Examples](#-usage-examples)
4. [Implementation Guide](#-implementation-guide)
5. [Complete Script](#-complete-script)
6. [Bonus Features](#-bonus-features)

---

## **📝 Project Overview**
This Bash script generates customizable multiplication tables with:
- **Flexible ranges** (full 1-10 or custom range)
- **Input validation** for numbers and ranges
- **Multiple loop styles** (list and C-style)
- **User-friendly output formatting**

---

## **✨ Script Features**

### **Core Functionality**
- Interactive prompts for number and range selection
- Handles invalid inputs gracefully
- Displays tables in clear format
- Supports both ascending and descending order

### **Technical Components**
```bash
# List form loop example
for i in {1..10}; do
    echo "$num x $i = $((num*i))"
done

# C-style loop example
for ((i=1; i<=10; i++)); do
    echo "$num x $i = $((num*i))"
done
```

---

## **🖥️ Usage Examples**

### **Full Table (1-10)**
```bash
Enter a number: 5

Choose table type:
1) Full table (1-10)
2) Custom range
Your choice: 1

5 x 1 = 5
5 x 2 = 10
...
5 x 10 = 50
```

### **Custom Range**
```bash
Enter a number: 3

Choose table type:
1) Full table (1-10)
2) Custom range
Your choice: 2

Enter start (1-10): 4
Enter end (1-10): 7

3 x 4 = 12
3 x 5 = 15
3 x 6 = 18
3 x 7 = 21
```

### **Invalid Range Handling**
```bash
Invalid range (8-2)! Showing full table instead.
3 x 1 = 3
...
3 x 10 = 30
```

---

## **🛠️ Implementation Guide**

### **1. Input Validation**
```bash
while true; do
    read -p "Enter a number: " num
    [[ $num =~ ^[0-9]+$ ]] && break
    echo "Invalid number!"
done
```

### **2. Range Selection**
```bash
read -p "Choose table type [1/2]: " choice
case $choice in
    1) start=1; end=10 ;;
    2) 
        read -p "Enter start: " start
        read -p "Enter end: " end
        (( start > end )) && { echo "Invalid range!"; start=1; end=10; }
    ;;
esac
```

### **3. Table Generation**
```bash
# Ascending order
for ((i=start; i<=end; i++)); do
    printf "%d x %d = %d\n" $num $i $((num*i))
done

# Descending order (bonus)
for ((i=end; i>=start; i--)); do
    printf "%d x %d = %d\n" $num $i $((num*i))
done
```

---

## **📜 Complete Script**
```bash
#!/bin/bash

# Print header
echo -e "\n\033[1;34mMultiplication Table Generator\033[0m"

# Get valid number input
while true; do
    read -p "Enter a number: " num
    [[ $num =~ ^[0-9]+$ ]] && break
    echo -e "\033[31mInvalid number! Try again.\033[0m"
done

# Table type selection
echo -e "\nChoose table type:"
echo "1) Full table (1-10)"
echo "2) Custom range"
while true; do
    read -p "Your choice [1/2]: " choice
    case $choice in
        1) start=1; end=10; break ;;
        2)
            read -p "Enter start (1-10): " start
            read -p "Enter end (1-10): " end
            if (( start < 1 || end > 10 || start > end )); then
                echo -e "\033[33mInvalid range! Defaulting to full table.\033[0m"
                start=1; end=10
            fi
            break
        ;;
        *) echo -e "\033[31mInvalid choice!\033[0m" ;;
    esac
done

# Order selection (bonus)
read -p "Display order [a]scending/[d]escending: " order
[[ $order == "d" ]] && dir="descending" || dir="ascending"

# Generate table
echo -e "\n\033[1;32m$dir multiplication table for $num ($start-$end):\033[0m"
if [[ $order == "d" ]]; then
    for ((i=end; i>=start; i--)); do
        printf "%d x %d = %d\n" $num $i $((num*i))
    done
else
    for ((i=start; i<=end; i++)); do
        printf "%d x %d = %d\n" $num $i $((num*i))
    done
fi
```

---

## **🎁 Bonus Features**

### **1. Order Selection**
```bash
a) Ascending (1 → 10)
d) Descending (10 → 1)
```

### **2. Colorized Output**
- Error messages in red
- Success messages in green
- Headers in blue

### **3. Continuous Operation**
```bash
read -p "Generate another table? [y/n]: " again
[[ $again == "y" ]] && exec "$0"
```

---

## Screenshots

<img width="449" alt="Snipaste_2025-07-05_12-26-16" src="https://github.com/user-attachments/assets/ef1eb292-dbff-4eb3-a3dd-bada63c52aeb" />


<img width="443" alt="Snipaste_2025-07-05_12-25-01" src="https://github.com/user-attachments/assets/54a9aaf7-c0e4-4e25-9456-05f751a54d8b" />


<img width="536" alt="Snipaste_2025-07-05_12-22-56" src="https://github.com/user-attachments/assets/b5e08db2-f31a-4ce4-accd-d3b0a30b6506" />


<img width="595" alt="Snipaste_2025-07-05_12-22-31" src="https://github.com/user-attachments/assets/09cfc64f-7036-4349-9e89-9ad36be46e82" />


<img width="567" alt="Snipaste_2025-07-05_12-21-55" src="https://github.com/user-attachments/assets/8671c02e-4b7b-4687-bf28-31179748f871" />


<img width="567" alt="Snipaste_2025-07-05_12-21-55" src="https://github.com/user-attachments/assets/01e3fc94-f843-4f85-96d0-69d90f8e4046" />



## **📚 Learning Resources**
- [Bash For Loops](https://linuxize.com/post/bash-for-loop/)
- [Arithmetic Expansion](https://www.gnu.org/software/bash/manual/html_node/Arithmetic-Expansion.html)
- [Input Validation](https://www.shell-tips.com/bash/input-validation/)

```bash
# Make script executable
chmod +x multitable.sh

# Run script
./multitable.sh
```

**Pro Tip**: Use `printf` instead of `echo` for consistent formatting across different systems!
