# Exploiting Basic OS Command Injection

## Lab Information

- **Challenge Name:** OS Command Injection – Simple Case  
- **Classification:** OS Command Injection  
- **Skill Level:** Apprentice  
- **Status:** Resolved

## Objective

Target an OS command injection vulnerability present in the stock checking component. The goal is to run the `whoami` system command to identify the user privilege level under which the web application process executes.

---

## Vulnerability Analysis

The application's stock checker concatenates user input directly into system commands without executing appropriate sanitization. Because of this design choice, appending shell metacharacters to the `storeId` parameter allows an attacker to run arbitrary system shell commands in the server environment.

---

## Exploitation Steps

1. Navigate to a product detail view.
2. Select the **Check Stock** button and capture the transaction using Burp Suite.
3. Relay the captured HTTP request to Burp Repeater.
4. Append the payload to the `storeId` parameter.
5. Transmit the edited request.
6. Inspect the server's HTTP response.
7. Verify that the response contains the execution output of the command, confirming the injection vulnerability.

---

## Payload Used

```text
1|whoami
```

---

## Result

The application executed the injected system command and returned the active operating system user running the web services, demonstrating a critical OS Command Injection vulnerability.

---

## Screenshots

### Command Execution

![Command Execution](images/executed_system_command.png)

### Lab Solved

![Lab Solved](images/solved_evidence.png)

---

## Impact Assessment

An attacker can execute arbitrary operating system commands on the target host. 

Possible impacts include:

- Sensitive information disclosure.
- Unauthorized file system access.
- Local system credential theft.
- Full remote code execution.
- Compromise of the host server.

---

## Remediation and Mitigation

- Avoid invoking shell-level OS commands using user-controlled parameters.
- Utilize secure, native programming APIs instead of shell execution helpers.
- Implement robust input validation and cleaning filters.
- Enforce strict allowlist checks on all parameters.
- Restrict system process privileges using low-privileged service accounts.

---

## Summary Takeaway

Never feed user-provided inputs directly into operating system commands. Even a simple parameter like `storeId` can be abused to achieve remote code execution if strict input sanitization is not enforced.