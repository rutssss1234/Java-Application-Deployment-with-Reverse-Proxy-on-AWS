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

