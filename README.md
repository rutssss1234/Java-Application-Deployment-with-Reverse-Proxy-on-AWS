# Java-Application-Deployment-with-Reverse-Proxy-on-AWS
Java Application Deployment with Reverse Proxy on AWS is a project where a Student Registration web app is hosted on an EC2 server using Tomcat, connected to an Amazon RDS MySQL database, and securely accessed through a reverse proxy server. Only the proxy is public, ensuring secure and controlled application access.
📌 Project Overview
This project demonstrates the migration of a legacy Java-based Student Registration Web Application to a secure AWS cloud infrastructure.
The main objective was to eliminate security risks caused by direct backend exposure by implementing a Reverse Proxy Architecture.
Using Nginx as a reverse proxy and Apache Tomcat as the backend application server, the system ensures that:
Backend services are not publicly exposed
Database access is restricted
All traffic flows through a controlled entry point

🏗 Architecture
https://github.com/rutssss1234/Java-Application-Deployment-with-Reverse-Proxy-on-AWS/blob/main/Screenshot%202026-05-01%20111324.png?raw=trueTraffic FlowTraffic Flow

🔁 Traffic Flow
User → Nginx (Proxy Server) → Tomcat (Backend Server) → RDS (MySQL)

📊 Explanation
-User accesses application via Proxy Public IP (Port 80)
-Nginx forwards requests to Backend Server (Port 8080)
-Tomcat processes the request
-Data is stored/retrieved from Amazon RDS (MySQL)
-Backend and Database are not publicly accessible

🛠 Technology Stack
Layer	       Technology
Cloud	AWS    (EC2, RDS, VPC, Security Groups)
Reverse Proxy	Nginx
Application Server	Apache Tomcat 9
Backend Language	Java (OpenJDK 11)
Database	Amazon RDS (MySQL 8.0)
JDBC Driver	MySQL Connector/J

🚀 Deployment Steps
1️⃣ Infrastructure Setup
Created 2 EC2 Instances:

Proxy Server (Public)
Backend Server (Private-like access)
Created RDS MySQL Database

Configured Security Groups:

Proxy → Public access (Port 80)
Backend → Only accessible from Proxy (Port 8080)
RDS → Only accessible from Backend (Port 3306)

2️⃣ Database Setup
CREATE DATABASE studentdb;
USE studentdb;

CREATE TABLE students (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    address VARCHAR(200),
    age INT,
    qualification VARCHAR(100),
    percentage DOUBLE,
    year_passed INT
);

3️⃣ Backend Deployment (Tomcat)
Installed Java (OpenJDK 11)
Installed Apache Tomcat 9
Deployed student.war in /webapps
Added MySQL Connector JAR to /lib
Configured database connection:
db.url=jdbc:mysql://<RDS-ENDPOINT>:3306/studentdb
db.user=admin
db.password=********

4️⃣ Reverse Proxy Configuration (Nginx)
location /student {
    proxy_pass http://<BACKEND_PRIVATE_IP>:8080/student;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
}

🔒 Security Implementation
✔ Backend EC2 is not publicly accessible ✔ Only Proxy can access Backend 
✔ RDS accepts traffic only from Backend ✔ Direct access to backend results in timeout

🌐 Application Access
http://<Proxy-Public-IP>/student

📸 Screenshots

✅ Running EC2 Instances
https://github.com/rutssss1234/Java-Application-Deployment-with-Reverse-Proxy-on-AWS/blob/640fce8779ea8f60ef3f2ef06646a10d4a4c956d/running%20backend%20server.jpeg

✅ Application UI via Proxy
https://github.com/rutssss1234/Java-Application-Deployment-with-Reverse-Proxy-on-AWS/blob/cf65c7e4a4464f5b255b585a7baddc26d266ad31/%E2%9C%85%20Application%20UI%20via%20Proxy.jpeg

✅ Application UI via Proxy Successfully Done










