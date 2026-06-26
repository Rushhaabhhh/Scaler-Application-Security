# Scaler Application Security Coursework

This repository contains the coursework, lab writeups, and secure code review assignments completed for the **Scaler Application Security** program.

---

## 📁 Repository Structure

```text
├── Code-Review-Assignment/
│   ├── supportdesk-app/                     # Target vulnerable flask application
│   ├── report_generator.py                  # Python script generating the HTML and PDF report
│   ├── report.html                          # Beautiful HTML report
│   ├── Secure_Code_Review_Report.pdf        # Production-grade compiled PDF report
│   ├── bandit_results.txt                   # Raw Bandit SAST results
│   ├── semgrep_results.txt                  # Raw Semgrep SAST results
│   └── Secure Code Review Assignment...pdf  # Instructions and guidelines
│
├── WriteUps/                                # Hands-on vulnerability writeups
│   ├── API_Testing/
│   ├── Access_Control/
│   ├── Authentication/
│   ├── Business_Logic_Vulnerabilities/
│   ├── CSRF/
│   ├── JWT/
│   ├── OS-Command-Injection/
│   ├── SQL/
│   ├── SSRF/
│   ├── SSTI/
│   ├── XSS/
│   └── XXE/
│
└── .gitignore                               # Git ignore rules for clean commits
```

---

## 🛡️ Secure Code Review Assignment

The code review assignment focuses on auditing the **Scaler Support Desk** (a Flask-based ticket system). It combines automated Static Application Security Testing (SAST) using **Semgrep** and **Bandit** with manual line-by-line verification.

### Key Highlights of the Report
- **13 Total Audited Findings**
- **10 True Positives (TP)**: Verified vulnerabilities including SQL Injection, OS Command Injection, Path Traversal, Weak Cryptographic Hashing, IDOR, Race Conditions, Hardcoded Secrets, and Missing CSRF Protections.
- **3 False Positives (FP)**: Flagged sections that manual inspection proved secure due to strict allowlists, dictionary lookup checks, and path normalization logic.
- **Comprehensive Details**: Every finding contains a description, vulnerable code snippets, Bandit/Semgrep outputs, root-cause explanation, impact assessment, and ready-to-deploy remediated code snippets.

---

## 🚀 Running the Localhost Server

To preview the interactive and beautiful HTML report (`report.html`) locally:

1. Navigate to the assignment folder:
   ```bash
   cd Code-Review-Assignment
   ```
2. Start a Python HTTP server:
   ```bash
   python3 -m http.server 8080
   ```
3. Open your browser and navigate to:
   ```text
   http://localhost:8080/report.html
   ```

---

## 📄 Re-generating the HTML & PDF Report

If you update `report_generator.py`, you can regenerate both the HTML report and the PDF report automatically.

1. Ensure you have **Google Chrome** installed (required for printing the PDF headlessly).
2. Run the generator script:
   ```bash
   python3 report_generator.py
   ```
3. This will overwrite `report.html` and compile the new PDF `Secure_Code_Review_Report.pdf` via Headless Chrome.

---

## 📝 Technical Lab Writeups (`/WriteUps`)

The `WriteUps` directory contains thorough writeups detailing practical exploits and secure remediation steps for labs covering the OWASP Top 10 web vulnerabilities. Key sections include:

- **Authentication & JWT**: Breaking authentication flows, signature bypasses, and token manipulation.
- **SQL & Command Injection**: Automating SQL exploitation (including blind time-based injection) and OS-level remote command execution.
- **CSRF & XSS**: Stored and Reflected Cross-Site Scripting, along with Cross-Site Request Forgery bypasses.
- **SSRF & SSTI**: Server-side request manipulation, local network mapping, and server-side template execution.
- **API & Access Control**: Identifying Broken Object-Level Authorization (BOLA/IDOR), path traversal, and business logic flaws.
