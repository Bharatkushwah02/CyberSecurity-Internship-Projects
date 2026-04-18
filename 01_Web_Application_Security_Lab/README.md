🕸️ Web Application Security Lab (OWASP Top 10)
This project is a dedicated security research environment built during my Cyber Security internship at Next Afield. The goal is to systematically identify, exploit, and remediate vulnerabilities listed in the OWASP Top 10


🛠️ Infrastructure & Setup
The lab is fully containerized using Docker to ensure process isolation and a safe testing environment.


📦 Applications Included:
DVWA (Damn Vulnerable Web App): PHP/MySQL based lab for core vulnerability testing.
OWASP Juice Shop: A modern Node.js application for complex security scenarios.
WebGoat: A deliberate insecure application for Java-based security lessons.


🚀 Deployment Instructions
Ensure Docker Desktop is running on your host machine.
Clone this repository and navigate to this directory.
Deploy the lab using:

```bash
docker-compose up -d
```
Access the labs via browser:
DVWA: 
``` http://localhost:8081 ```
(Default Creds: admin / password)
Juice Shop:``` http://localhost:3000  ```



🔍 Vulnerabilities Reproduced (Proof of Concept)
1. SQL Injection (SQLi)
Vector: User ID input field.

Payload: ' OR '1'='1

Description: By injecting a tautology, the backend SQL query was manipulated to return all records from the users table, bypassing individual ID lookup.

Status: ✅ Successfully exploited.



2. Cross-Site Scripting (XSS) - Reflected
Vector: Name input field.

Payload: <script>alert("Hacked by Bharat")</script>

Description: Malicious JavaScript was successfully executed in the context of the user's session because the application failed to sanitize user input before rendering it on the page.



Status: ✅ Successfully exploited.
📝 Deliverables Checklist (Internship Progress)
[x] Docker-based Lab Setup
[x] SQLi Lab Reproduction & Documentation
[x] XSS Lab Reproduction & Documentation
[ ] Burp Suite Interception Logs
[ ] Secure Code Remediation (Before/After)
[ ] Final Security Assessment Report
