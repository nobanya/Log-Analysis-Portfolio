# Intro to Syslog Analysis on Linux 

## Introduction 
This project introduces foundational syslog analysis techniques on Linux systems. Syslog is a widely used logging standard responsible for capturing messages from system services and applications. Through this project, learners will explore syslog configuration files, review log data, and perform basic analysis to support troubleshooting and security monitoring activities.

## Requirements
- Basic knowledge of Linux system administration concepts
- Experience using the Linux command line
- Access to a Linux system (Ubuntu preferred)

## Lab Environment and Tools
- Ubuntu 20.04 or newer (or any Linux distribution with syslog enabled)
- Permission to view system log files (commonly found in /var/log/)

---

## Exercises

### Exercise 1: Reviewing Syslog Configuration

**Steps:**

1. Open the syslog configuration file in a text editor:
    ```bash
    sudo nano /etc/rsyslog.conf
    ```
2. Examine the configuration settings to see how syslog is set up.
3. Locate and review the different logging facilities and where their logs are written.

**Expected Output**: Familiarity with syslog configuration components, including facilities and log file destinations..

---

### Exercise 2: Accessing Syslog Files

**Steps:**

1. Change to the syslog directory:
    ```bash
    cd /var/log/
    ```
2. Display the available log files to see what data is being collected by the system:
    ```bash
    ls -l
    ```
3. View the primary syslog file using `less` or `cat`:
    ```bash
    less syslog
    ```

**Expected Output**: Visibility into the available syslog files and a preview of the main syslog content.

---

### Exercise 3: Filtering Syslog Entries

**Steps:**

1. Use grep to search syslog entries for a specific date:
    ```bash
    grep 'Jun 12' syslog
    ```
2. Filter entries related to a particular service or process, such as sshd:
    ```bash
    grep 'sshd' syslog
    ```
3. Combine multiple filters to isolate the exact information suchas sshd activity on a specific date:
    ```bash
    grep 'Jun 12' syslog | grep 'sshd'
    ```

**Expected Output**: A refined set of syslog entries matching the selected filters, demonstrating targeted log analysis.

---

### Exercise 4: Examining Authentication Logs

**Steps:**

1. Open the authentication log file using `less` or `cat`:
    ```bash
    less auth.log
    ```
2. Identify various authentication-related events, such as successful logins, failed login attempts, and user changes.
3. Review timestamps, usernames, and source IP addresses associated with each event.

**Expected Output**: Clear insight into authentication activity, highlighting both successful and failed login behavior.

---

### Exercise 5: Aggregating Log Information

**Steps**:

1. Use awk to count failed sshd login attempts by source IP address:
    ```bash
    awk '/sshd/ && /Failed password/ {print $11}' auth.log | sort | uniq -c | sort -nr
    ```
2. Summarize the number of successful sshd logins grouped by user account:
    ```bash
    awk '/sshd/ && /Accepted password/ {print $9}' auth.log | sort | uniq -c | sort -nr
    ```
3. Identify the most common message types recorded in syslog:
    ```bash
    awk '{print $6}' syslog | sort | uniq -c | sort -nr
    ```

**Expected Output**: Aggregated results showing login attempts per IP, successful logins by user, and the most frequent syslog message categories.

---

### Outcome
Completing these exercises provides practical experience working with Linux syslog data. These skills are essential for diagnosing system issues, monitoring authentication activity, and supporting security investigations in real-world environments.
