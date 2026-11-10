# Task 4 – Setup and Use a Firewall on Windows 11

## 1. Objective
The objective of this task is to configure and test basic firewall rules to allow or block incoming network traffic using Windows Defender Firewall.

## 2. Tools Used
- Windows 11
- Windows Defender Firewall
- Windows PowerShell

## 3. Introduction
A firewall is a security system that monitors incoming and outgoing network traffic. It allows or blocks traffic based on predefined security rules.

## 4. Implementation

### Step 1: Check Firewall Status
Used PowerShell to check the current firewall profiles and existing firewall rules.

Command:
`Get-NetFirewallProfile`

### Step 2: Create a Firewall Block Rule
Created an inbound firewall rule to block TCP traffic on port 23, which is commonly used by Telnet.

Command:
`New-NetFirewallRule -DisplayName "Task4-Block-Telnet-23" -Direction Inbound -Protocol TCP -LocalPort 23 -Action Block -Profile Any`

### Step 3: Verify the Firewall Rule
Checked the firewall rule to confirm that it was enabled and configured correctly.

Command:
`Get-NetFirewallRule -DisplayName "Task4-Block-Telnet-23"`

Verified the protocol and port using:

`Get-NetFirewallRule -DisplayName "Task4-Block-Telnet-23" | Get-NetFirewallPortFilter`

Result:
- Protocol: TCP
- Local Port: 23
- Direction: Inbound
- Action: Block

### Step 4: Test the Connection
Used the following command to test TCP connectivity to localhost on port 23.

`Test-NetConnection -ComputerName localhost -Port 23`

Result:
- PingSucceeded: True
- TcpTestSucceeded: False

The TCP connection was unsuccessful. This result alone does not confirm that the firewall caused the failure, as no listening Telnet service was established for the test.

### Step 5: Remove the Temporary Rule
Removed the temporary firewall rule after testing.

Command:
`Remove-NetFirewallRule -DisplayName "Task4-Block-Telnet-23"`

Verified removal using:

`Get-NetFirewallRule -DisplayName "Task4-Block-Telnet-23" -ErrorAction SilentlyContinue`

No output was returned, confirming that the temporary rule was removed.

## 5. How a Firewall Filters Traffic
A firewall monitors network traffic and checks it against configured rules. It allows permitted traffic and blocks unwanted or unauthorized connections.

## 6. Outcome
Successfully created, configured, verified, and removed a Windows Firewall rule for blocking incoming TCP traffic on port 23.

## 7. Conclusion
This task helped me understand basic firewall configuration, network traffic filtering, port blocking, and firewall rule management using Windows PowerShell.
