#  Introductory Apache Web Server Log Analysis

## Introduction
This project introduces the core concepts of log analysis through hands on interaction with Apache web server logs. Apache access and error logs provide detailed insight into web activity and are commonly used to investigate security events, analyze traffic behavior, and diagnose operational issues. Upon completing this project, learners will be able to review log entries, identify meaningful patterns, and extract useful information from Apache logs.

## Requirements
- Fundamental knowledge of web servers and HTTP communication
- Comfort working in a Linux command-line environment
- An Apache web server installed locally or on a virtual machine


## Lab Set-up and Tools
- Ubuntu 22.04 or newer (or any Linux distribution running Apache)
- Apache web server installed and operational
- Access to Apache log files (commonly stored in `/var/log/apache2/`)

## Exercises

### Exercise 1: Locating Apache Log Files

**Steps:**

1. Launch a terminal session on your Linux machine.
2. Change directories to the Apache log location:
    ```bash
    cd /var/log/apache2/
    ```
3. List the log files to display the available logs:
    ```bash
    ls -l
    ```

**Expected Output**: A directory listing that includes files such as `access.log` and `error.log`.

---

### Exercise 2: Understanding Access Logs

**Steps:**

1. Open the access log file using `less` or `cat`:
    ```bash
    less access.log
    ```
2. Examine the structure of individual log entries, which usually contain the source IP address, timestamp, HTTP request method, requested resource, response status code, and user-agent string.
3. Select several entries and identify each component within the log line

**Expected Output**: Familiarity with the standard Apache access log format, including IP addresses, timestamps, HTTP methods, URLs, response codes, and user agents.

---

### Exercise 3: Filtering Access Log 

**Steps:**

1. Use grep to filter & locate log entries associated with a specific IP address::
    ```bash
    grep '192.168.1.100' access.log
    ```
2. Filter log entries that returned a specific HTTP status code, such as 404:
    ```bash
    grep ' 404 ' access.log
    ```
3. Combine filters to find 404 responses originating from a particular IP:
    ```bash
    grep '192.168.1.100' access.log | grep ' 404 '
    ```

**Expected Output**: A filtered list of log entries matching the specified criteria, displaying how to extract specific data from log files.

---

### Exercise 4: Reviewing Error Logs

**Steps:**

1. Open the Apache error log file using `less` or `cat`:
    ```bash
    less error.log
    ```
2. Identify various error messages such as missing files, script execution failures, or permission-related issues.
3. Review timestamps and repetition patterns to determine whether errors are isolated or recurring.

**Expected Output**: Improved understanding of error log entries and the types of issues they can reveal.

---

### Exercise 5: Aggregating & Summarizing Log Data

**Steps:**

1. Use awk to count the number of requests originating from each IP address:
    ```bash
    awk '{print $1}' access.log | sort | uniq -c | sort -nr
    ```
2. Generate a summary of requests per day:
    ```bash
    awk '{print $4}' access.log | cut -d: -f1 | sort | uniq -c
    ```
3. Determine which URLs were requested most frequently:
    ```bash
    awk '{print $7}' access.log | sort | uniq -c | sort -nr
    ```

**Expected Output**: Aggregated results highlighting request volume of requests per IP address, the number of requests per day, and the most requested URLs.

---

### Outcome
By completing these exercises, learners develop practical experience working with Apache logs, building skills that are essential for detecting security issues, analyzing web traffic trends, and troubleshooting web server problems in real world environments.
