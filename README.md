
# A PrestaShop Issue: Attack and Defence

## Malware Defense and Application Security  
**Final Project Report for INSE-6140**  
**Presented to:** Dr. Makan Pourzandi  
**Presented by:** WCS  

**Team Members:**  
- Pierre Watine (40027675)  
- Anik Chowdhury (40275019)  
- Akash Saha (40233587)  

---

## 📄 Project Overview

This project focuses on identifying and mitigating a stored **Cross-Site Scripting (XSS)** vulnerability in **PrestaShop**, an open-source e-commerce platform. By uploading a malicious **SVG** image, attackers can execute harmful scripts, leading to session hijacking and credential theft.

---

## 🛠️ Tools & Technologies

- **Operating System:** Kali Linux 2023.4  
- **Web Server:** Apache 2.4.58 (via XAMPP 8.2.12)  
- **Database:** MariaDB 10.4.32  
- **Security Testing Tools:**  
  - [OWASP ZAP](https://www.zaproxy.org/) – Dynamic Analysis  
  - [Nessus](https://www.tenable.com/products/nessus) – Vulnerability Scanning  
  - [Nikto](https://cirt.net/Nikto2) – Web Server Scanner  
  - [SQLmap](https://sqlmap.org/) – SQL Injection Testing  
  - [Burp Suite](https://portswigger.net/burp) – Web Proxy  
  - [RATS](https://security.web.cern.ch/tools/rats.shtml) – Static Analysis  
  - [Snyk](https://snyk.io/) – Static Code Analysis  
  - [Horusec](https://horusec.io/) – Static Code Analysis  

---

## 🔍 Methodology

1. **Setup:** Deployed PrestaShop on a local Apache server with a MariaDB backend.  
2. **Scanning:** Conducted vulnerability scans using OWASP ZAP, Nessus, and Nikto.  
3. **Static Analysis:** Used RATS, Snyk, and Horusec to analyze source code.  
4. **Exploit Testing:** Uploaded crafted **SVG** files to test for stored XSS vulnerabilities.  
5. **Manual Testing:** Employed Burp Suite to manipulate web requests and analyze responses.  

---

## ⚠️ Identified Vulnerability

- **Type:** Stored Cross-Site Scripting (XSS)  
- **Vector:** Malicious **SVG** file upload via the PrestaShop back office.  
- **Impact:** High (Session Hijacking, Credential Theft)  
- **Likelihood:** Low (Requires back-office user interaction)

**Proof of Concept (PoC):**  
- Uploaded an SVG file containing a script payload.  
- Upon accessing the product edit page, the script executes, potentially stealing session cookies.  

---

## 🛡️ Proposed Mitigations

### 1️⃣ Disable SVG Uploads  
**Action:** Remove SVG from allowed file formats in `config/config.php`.  
**Effect:** Blocks SVG uploads, reducing the attack surface.

### 2️⃣ Implement SVG Sanitization  
**Action:** Integrate a secure sanitization library like [svg-sanitizer](https://github.com/darylldoyle/svg-sanitizer).  
**Effect:** Filters out malicious scripts within SVG files before upload.  

---

## 📂 Project Structure

```
├── images/
│   ├── xss.svg           # Malicious SVG with script
│   ├── no-xss.svg        # Clean SVG (control)
│   └── disguisedxss.svg  # Bypasses naive sanitizers
├── reports/
│   ├── owasp-zap-report.html
│   ├── nessus-scan-report.pdf
│   └── nikto-scan-results.txt
├── src/
│   └── upload.php        # Modified file handling upload sanitization
├── README.md
└── Final_Project_Report.pdf
```

---

## 📊 Results

- **OWASP ZAP:** Detected missing security headers (anti-CSRF, anti-clickjacking).  
- **Static Analysis:** Limited findings, but hints of potential injection points.  
- **Dynamic Analysis:** Confirmed stored XSS via SVG uploads.  
- **Risk Evaluation:**  
  - **Impact:** High  
  - **Likelihood:** Low  
  - **Overall Risk:** Medium  

---

## 🔎 Further Improvements

- Implement **Content Security Policy (CSP)** headers.  
- Explore deeper for **SQL Injection** vulnerabilities.  
- Perform broader vulnerability scanning on additional modules/plugins.

---

## 📚 References

1. Ağalarov, M. *Prestashop 8.0.4 - Cross-Site Scripting (XSS)*. [Exploit DB](https://www.exploit-db.com/exploits/51563)  
2. Norris, A. *SVG-Sanitizer*. [GitHub](https://github.com/alnorris/SVG-Sanitizer)  
3. Doyle, D. *svg-sanitizer*. [GitHub](https://github.com/darylldoyle/svg-sanitizer)  

---

## 💼 License

This project is for educational purposes as part of the **INSE-6140 Malware Defense and Application Security** course.  

---

## 🤝 Acknowledgements

Special thanks to **Dr. Makan Pourzandi** for guidance and support throughout this project.
