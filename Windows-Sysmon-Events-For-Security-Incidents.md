#  Investigating Security Incidents Using Windows Sysmon Logs

## Introduction

This lab introduces hands on analysis of Windows Sysmon (System Monitor) events to detect and investigate security-related activity. Sysmon is an advanced Windows service that records detailed system behavior such as process execution, network communication, and file activity, directly into Windows Event Logs. By reviewing these logs, analysts can uncover suspicious behavior and indicators of compromise.

## Requirements

- Basic knowledge of the Windows operating system and core components
- Familiarity with introductory cybersecurity principles
- A system running Windows 10 or newer (using a virtual machine is strongly recommended)
- Internet access to download required tools

## Lab Environment and Tools

 **Install Sysmon**:
   - Download Sysmon from the [Sysinternals website](https://docs.microsoft.com/en-us/sysinternals/downloads/sysmon).
   - Extract the downloaded file.

**Configure Sysmon**:
   - Download a Sysmon configuration file. The SwiftOnSecurity configuration available on [GitHub](https://github.com/SwiftOnSecurity/sysmon-config) can be used.
   - Open Command Prompt with administrative privileges and navigate to the Sysmon directory.
   - Install Sysmon using the configuration file:
     ```bash
     sysmon -accepteula -i sysmonconfig-export.xml
     ```

 **Tools**:
   - Sysmon (System Monitor)
   - Event Viewer (built-in Windows tool)
   - PowerShell (built-in Windows tool)

## Exercises

### Exercise 1: Confirm Sysmon Is Running Properly

 **Objective**: Verify that Sysmon has been installed correctly and is actively running.

 **Steps**:
   1. Open Event Viewer from the Start menu.
   2. Navigate to `Applications and Services Logs -> Microsoft -> Windows -> Sysmon`.
   3. Review recent log entries to confirm that Sysmon is logging events.

 **Expected Output**: Multiple Sysmon events should be visible, confirming that monitoring is enabled.

---

### Exercise 2: Review Process Creation Events

1. **Objective**: Detect suspicious process execution events..

2. **Steps**:
   - In Event Viewer, go to `Applications and Services Logs -> Microsoft -> Windows -> Sysmon -> Operational`.
   - Locate events with Event ID 1, which represent process creation.
   - Examine event details, pay close attention to:
     - Parent process name
     - Process name
     - Command line parameters

3. **Expected Output**: Identification of unusual or unexpected processes, including abnormal execution paths or suspicious command-line usage.

---

### Exercise 3: Analyze Network Connections

1. **Objective**: Identify suspicious or unauthorized network activity.

2. **Steps**:
   - In Event Viewer, navigate to `Applications and Services Logs -> Microsoft -> Windows -> Sysmon -> Operational`.
   - Search for events with Event ID 3, which log network connections.
   - Review the following details:
     - Source IP and port
     - Destination IP and port
     - Process responsible for initiating connection

3. **Expected Output**: Detection of unexpected outbound connections or communication with potentially malicious IP addresses..

---

### Exercise 4: Examine File Creation Events

1. **Objective**: Monitor file creation for signs of malicious behavior.

2. **Steps**:
   - In Event Viewer, go to `Applications and Services Logs -> Microsoft -> Windows -> Sysmon -> Operational`.
   - Look for Event ID 11, which records file creation activity
   - Review details of events such as:
     - File path
     - File name
     - Process that created the file

3. **Expected Output**: Identified abnormal file creation activity, particularly in sensitive directories or initiated by untrusted processes.

---

### Exercise 5: Inspect Image Load Events

1. **Objective**: Detect suspicious DLL or EXE Image load.

2. **Steps**:
   - In Event Viewer, go to `Applications and Services Logs -> Microsoft -> Windows -> Sysmon -> Operational`.
   - Fiind events with `Event ID 7` which indicate image load.
   - Examine event details such as:
     - Image path
     - Processes that load the image

3. **Expected Output**: Identification of unexpected or unauthorized image loads that may signal techniques such as DLL injection.

---

## Conclusion

Upon completing this lab, you will have practical experience using Sysmon and Event Viewer to monitor and analyze Windows system activity. Regular review of Sysmon logs strengthens an analyst’s ability to detect suspicious behavior, investigate security incidents, and improve overall endpoint visibility within Windows environments.
