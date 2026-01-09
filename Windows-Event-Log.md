# Investigating Security Activity Using Windows Event Logs

## Introduction
This project focuses on building practical skills in reviewing and analyzing Windows Event Logs to identify potential security incidents. Windows event logging provides detailed visibility into system behavior, user authentication activity, and configuration changes. By completing this project, learners will gain practical experience accessing event logs, recognizing security-relevant events, and using log analysis techniques to support incident response efforts.

## Reqiurements
- Fundamental knowledge of the Windows operating system and administrative concepts
- Experience navigating Windows Event Viewer
- A Windows system running Windows 10 or newer

## Lab Environment and Tools
- Windows 10 or later
- Event Viewer
-  [Log Parser Studio](https://www.microsoft.com/en-us/download/details.aspx?id=24659) (for advanced log analysis)

  ---
  
## Exercises

### Exercise 1: Opening Windows Event Logs

**Steps:**

1. Launch Event Viewer by pressing Win + R, entering eventvwr, and pressing Enter`.
2. In the Event Viewer interface, expand Windows Logs and select System.
3. Review the system-generated events to become familiar with the types of activity logged by Windows.

**Expected Output**: Successful access to System logs and an understanding of common system level events.

---

### Exercise 2: Reviewing Security Event Logs

**Steps:**

1. Within Event Viewer, expand Windows Logs and click "Security".
2. Examine security-related events, paying close attention to logon attempts, account management, and policy changes.
3. Identify commonly used security Event IDs such as 4624 (successful logon) and 4625 (failed logon).

**Expected Output**: Awareness of security-focused event types and key Event IDs associated with authentication and account activity.

---

### Exercise 3: Filtering and Searching Logs

**Steps:**

1. In Event Viewer, select Filter Current Log from the right-hand pane.
2. Apply a filter to display only Security events with a specific Event ID, such as 4625 for failed logons.
3. Use the Find feature to search for events tied to a particular username or workstation.

**Expected Output**: A narrowed down event log view highlighting relevant security events for targeted investigation.

---

### Exercise 4: Reviewing Event Details

**Steps:**

1. Select an individual security event, such as a failed logon entry, and open its details.
2. Document important fields including timestamps, user accounts, source IP addresses, and error codes.
3. Correlate related events to identify activity patterns, such as repeated failed logons followed by a successful authentication.

**Expected Output**: Detailed insight into particular security events and their matching relationship to one another.

---

### Exercise 5: Advanced Log Analysis with Log Parser Studio

**Steps:**

1. Download and install [Log Parser Studio](https://www.microsoft.com/en-us/download/details.aspx?id=24659).
2. Launch Log Parser Studio and import a sample Windows event log file.
3. Execute built-in queries to analyze log data, such as identifying the most frequent sources of failed logon attempts:
    ```sql
    SELECT TOP 10 EXTRACT_TOKEN(TextData, 0, ' ') AS EventID, COUNT(*) AS EventCount
    FROM '[LOGFILEPATH]'
    WHERE EventID = 4625
    GROUP BY EventID
    ORDER BY EventCount DESC
    ```
4. Modify or create additional queries to extract specific security-related insights from the logs.

**Expected Output**: Enhanced visibility into event log data using Log Parser Studio with structured queries that summarize and highlight security activity.

---
### Outcome

Completing this project equips learners with practical experience analyzing Windows Event Logs in a security context. These skills are critical for detecting suspicious behavior, supporting incident investigations, and strengthening overall system security monitoring.
