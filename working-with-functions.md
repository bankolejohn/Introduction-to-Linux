# **Shell Scripting with Functions - AWS Automation Guide**

![Shell Scripting](https://miro.medium.com/v2/resize:fit:1400/1*_X8S7kXY4e8S6XUx8Q2z3w.png)

## **Table of Contents**
1. [Introduction](#-introduction)
2. [Function Basics](#-function-basics)
3. [Practical Implementation](#-practical-implementation)
4. [AWS Automation Example](#-aws-automation-example)
5. [Best Practices](#-best-practices)
6. [Cheat Sheet](#-cheat-sheet)

---

## **📝 Introduction**
This guide covers how to write modular shell scripts using functions to automate AWS infrastructure setup. Learn to create maintainable, robust scripts with proper error handling and environment management.

---

## **🛠️ Function Basics**

### **Syntax**
```bash
function_name() {
    # Commands
    return $status
}
```

### **Key Features**
- **Reusability**: Call functions multiple times
- **Modularity**: Isolate logical components
- **Readability**: Self-documenting through names
- **Error Handling**: Centralized validation

### **Calling Functions**
```bash
# Define first
validate_input() {
    [ "$#" -eq 1 ] || return 1
}

# Call later
validate_input "$@" || exit 1
```

---

## **💻 Practical Implementation**

### **1. Argument Validation**
```bash
check_arguments() {
    if [ "$#" -ne 1 ]; then
        echo "Usage: $0 <environment>"
        exit 1
    fi
}
```

### **2. Environment Handling**
```bash
setup_environment() {
    case "$1" in
        local)    echo "Local config" ;;
        testing)  echo "Test config" ;;
        prod*)    echo "Prod config" ;;
        *)        echo "Invalid env"; exit 2 ;;
    esac
}
```

### **3. Dependency Checks**
```bash
check_aws_cli() {
    command -v aws &>/dev/null || {
        echo "AWS CLI missing"
        return 1
    }
}
```

---

## **☁️ AWS Automation Example**

### **Complete Script Structure**
```bash
#!/bin/bash

# --- Functions ---
validate_input() {
    [ "$#" -eq 1 ] || {
        echo "Usage: $0 <local|testing|prod>"
        exit 1
    }
}

check_dependencies() {
    command -v aws &>/dev/null || {
        echo "Install AWS CLI first"
        exit 1
    }
}

setup_infra() {
    local env="$1"
    case "$env" in
        local)    aws configure set profile local ;;
        testing)  aws configure set profile test ;;
        prod*)    aws configure set profile prod ;;
    esac
    
    aws s3api create-bucket --bucket "data-${env}-bucket"
}

# --- Main ---
validate_input "$@"
check_dependencies
setup_infra "$1"
```

### **Key Components**
1. **Input Validation**
2. **Dependency Checks**
3. **Environment Configuration**
4. **Resource Creation**

---

## **🏆 Best Practices**

1. **Single Responsibility**
   - Each function should do one thing well

2. **Error Handling**
   ```bash
   create_bucket() {
       aws s3api create-bucket --bucket "$1" || {
           echo "Bucket creation failed"
           return 1
       }
   }
   ```

3. **Documentation**
   ```bash
   # Validates AWS credentials
   # Returns 0 if valid, 1 otherwise
   check_credentials() {
       aws sts get-caller-identity &>/dev/null
   }
   ```

4. **Testing**
   - Test functions individually
   - Verify error cases

---

## **📜 Cheat Sheet**

### **Function Operations**
| Command | Description |
|---------|-------------|
| `func(){ cmds; }` | Define function |
| `func arg1 arg2` | Call function |
| `local var=value` | Create local variable |
| `return N` | Exit with status |

### **Common Patterns**
```bash
# Early exit pattern
validate() || exit 1

# Error handling
command || {
    echo "Error occurred"
    return 1
}

# Default values
set_profile() {
    local profile="${1:-default}"
    # ...
}
```

---

## **📚 Resources**
- [Advanced Bash-Scripting Guide](https://tldp.org/LDP/abs/html/)
- [AWS CLI Documentation](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/index.html)
- [ShellCheck Linter](https://www.shellcheck.net/)

```bash
# Test your script
chmod +x script.sh
./script.sh testing
```

---

**Pro Tip**: Use `set -euo pipefail` at script start to:
- Exit on errors (`-e`)
- Treat unset variables as errors (`-u`)
- Catch pipeline failures (`pipefail`)

*"Good scripts are like good functions - they do one thing well."* - DevOps Proverb
