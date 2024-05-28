# Web Server Setup and Configuration

## Server Specifications

- **Server Name:** Web Server
- **Operating System:** Ubuntu 24.04 LTS (64-bit)
- **Type of Computer:** 64-bit (x86)
- **AMI ID:** ami-04b70fa74e45c3917
- **Type of Instance:** t2.small (Part of the t2 family)
- **Storage:** 20 Gigabytes SSD (gp3 type)

## Why We Chose This Server

We selected the t2.small instance for its balanced performance and cost-effectiveness. Here's why:

- **Sufficient Power:** The t2.small instance provides 1 processor and 2 gigabytes of memory, which is adequate for running ASP.NET and Next.js apps without being overly expensive.

- **Cost-Effectiveness:** At $0.0464 per hour, the t2.small instance offers a fair price-performance ratio for our needs.

- **Appropriate Resources:** ASP.NET and Next.js apps typically don't require extensive resources, especially in their initial stages. The t2.small instance offers enough power to handle them without wasting resources.

- **Operating System Compatibility:** Ubuntu 24.04 LTS is well-supported by a wide range of software commonly used by developers. It's user-friendly and prioritizes security, making it an ideal choice for our server setup.

- **Storage:** The 20 gigabyte SSD storage provided by the gp3 type offers ample space for hosting files and data associated with our apps. The gp3 type ensures consistent performance, and we have the flexibility to adjust storage capacity as needed.

## VPS Access

To access the VPS (Virtual Private Server):

1. **Navigate to Download Folder:**
   ```bash
   cd /path/to/Download
 
2. 
  ```bash
   ssh -i test-key.pem ubuntu@3.1.23.120



