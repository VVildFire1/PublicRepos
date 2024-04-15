# Application Layer Protocols

The Application Layer in the OSI model is the topmost layer that provides protocols for software applications to communicate over a network. Below is an overview of the various types of application layer protocols and their associated standard port numbers:

## Data Transfer Protocols
- **FTP (File Transfer Protocol)**: Used for transferring files between a client and server on a network.
  - Standard Ports: 20 (Data Transfer), 21 (Control Commands)
- **HTTP (HyperText Transfer Protocol)**: The foundation of data communication for the World Wide Web.
  - Standard Port: 80
- **HTTPS (HyperText Transfer Protocol Secure)**: The secure version of HTTP.
  - Standard Port: 443
  - also SSL and TLS are the same thing based on the name was changed around 2000 used for encryption 
- **TFTP (Trivial File Transfer Protocol)**: A simple, lockstep file transfer protocol with no authentication.
  - Standard Port: 69

## Authentication Protocols
- **Kerberos**: Network authentication protocol designed to provide strong authentication for client/server applications using secret-key cryptography.
  - Standard Port: 88
- **RADIUS (Remote Authentication Dial-In User Service)**: A networking protocol providing centralized Authentication, Authorization, and Accounting management for users.
  - Standard Ports: 1812 (Authentication), 1813 (Accounting)

## Network Service Protocols
- **DHCP (Dynamic Host Configuration Protocol)**: A network management protocol used on IP networks for dynamically assigning IP addresses and other network configuration parameters.
  - Standard Ports: 67 (Server), 68 (Client)
- **DNS (Domain Name System)**: The protocol for a hierarchical and decentralized naming system for computers, services, or other resources connected to the Internet or a private network.
  - Standard Port: 53

## Network Management Protocols
- **SNMP (Simple Network Management Protocol)**: An Internet Standard protocol for collecting and organizing information about managed devices on IP networks and modifying that information to change device behavior.
  - Standard Port: 161

## Audio/Visual Protocols
- **SIP (Session Initiation Protocol)**: A signaling protocol used for initiating, maintaining, and terminating real-time sessions that include voice, video, and messaging applications.
  - Standard Port: 5060
- **RTP (Real-time Transport Protocol)**: A network protocol for delivering audio and video over IP networks.
  - Standard Ports: Typically dynamically assigned from the range 16384 to 32767.

## Database Protocols
- **SQLNet**: A proprietary protocol used by Oracle databases for client-server database communication.
  - Default Port: 1521
- **ODBC (Open Database Connectivity)**: A standard API for accessing database management systems.
- **JDBC (Java Database Connectivity)**: An API for the Java programming language that defines how a client may access a database.

Each protocol is designed to fulfill specific data communication roles within various applications, ensuring reliable and secure transfer of information.
