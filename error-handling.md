# **Shell Scripting Error Handling Guide**  
*Building robust scripts with effective error management*

![Shell Script Error Handling](https://miro.medium.com/v2/resize:fit:1400/1*_X8S7kXY4e8S6XUx8Q2z3w.png)

## **Table of Contents**
1. [Error Handling Fundamentals](#-error-handling-fundamentals)
2. [Implementation Strategies](#-implementation-strategies)
3. [Practical Example: S3 Bucket Creation](#-practical-example-s3-bucket-creation)
4. [Key Techniques](#-key-techniques)
5. [Cheat Sheet](#-cheat-sheet)

---

## **🛡️ Error Handling Fundamentals**
Error handling in shell scripting involves anticipating and managing failures during execution. Common error sources include:
- Invalid user input
- Command execution failures
- Resource unavailability (files, network)
- Permission issues

**Why It Matters**:
- Prevents script crashes
- Provides actionable feedback
- Maintains system stability
- Enables automated recovery

---

## **🔧 Implementation Strategies**

### **1. Exit Status Checking**
```bash
aws s3api create-bucket --bucket "my-bucket"
if [ $? -ne 0 ]; then
    echo "Bucket creation failed!" >&2
    exit 1
fi
```

### **2. Conditional Logic**
```bash
if [ ! -f "config.txt" ]; then
    echo "Config file missing" >&2
    exit 1
fi
```

### **3. Trap Signals**
```bash
cleanup() {
    echo "Script interrupted! Cleaning up..."
    rm -f tempfile
    exit 1
}

trap cleanup SIGINT SIGTERM
```

### **4. Input Validation**
```bash
read -p "Enter bucket name: " bucket
if [[ ! "$bucket" =~ ^[a-z0-9-]+$ ]]; then
    echo "Invalid bucket name" >&2
    exit 1
fi
```

---

## **🪣 Practical Example: S3 Bucket Creation**
```bash
create_s3_buckets() {
    company="datawise"
    departments=("Marketing" "Sales" "HR" "Operations" "Media")
    
    for department in "${departments[@]}"; do
        bucket_name="${company}-${department}-Data-Bucket"
        
        # Check bucket existence
        if aws s3api head-bucket --bucket "$bucket_name" &>/dev/null; then
            echo "S3 bucket '$bucket_name' already exists."
        else
            # Create bucket with error handling
            if ! aws s3api create-bucket --bucket "$bucket_name" --region us-east-1; then
                echo "Failed to create '$bucket_name'" >&2
                return 1
            fi
            echo "Created '$bucket_name' successfully"
        fi
    done
}
```

**Key Improvements**:
1. Prevents duplicate bucket creation
2. Provides clear success/failure messages
3. Returns non-zero exit code on failure
4. Uses silent mode (`&>/dev/null`) for existence checks

---

## **🔑 Key Techniques**
| Technique | Command Example | Purpose |
|-----------|-----------------|---------|
| Exit Status | `$?` | Check command success |
| Error Redirection | `2> errors.log` | Capture stderr |
| Set Strict Mode | `set -euo pipefail` | Auto-exit on errors |
| Temporary Files | `trap "rm -f tmpfile" EXIT` | Cleanup on exit |

---

## **📜 Cheat Sheet**

### **Basic Error Handling**
```bash
# Exit on error
set -e

# Check command success
command || { echo "Failed"; exit 1; }

# Validate arguments
[ "$#" -eq 2 ] || { echo "Usage: $0 arg1 arg2"; exit 1; }
```

### **Advanced Patterns**
```bash
# Log errors with timestamp
error() { echo "[$(date)] ERROR: $*" >&2; }

# Retry mechanism
retry() {
    local n=1
    until "$@"; do
        ((n++))
        echo "Attempt $n failed"
        sleep 5
    done
}
```

---

## **📚 Resources**
- [Bash Error Handling Guide](https://linuxhint.com/bash_error_handling/)
- [AWS CLI Error Codes](https://docs.aws.amazon.com/cli/latest/reference/)
- [ShellCheck Linter](https://www.shellcheck.net/)

```bash
# Test your knowledge
./your_script.sh || echo "Script failed with exit code $?"
```

---

**Pro Tip**: Always test error scenarios by:
1. Providing invalid inputs
2. Revoking permissions
3. Disconnecting networks
4. Setting resource limits (`ulimit -n 10`)

*"Good error handling turns failures into feedback."* - DevOps Proverb
