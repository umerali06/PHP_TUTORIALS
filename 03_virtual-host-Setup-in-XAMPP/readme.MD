# Setting Up a Virtual Host in XAMPP:

This guide will take you step-by-step through the process of setting up Virtual Hosts in XAMPP for local web development. By the end of this guide, you will be able to create custom domains (like myproject.local) that point to different projects on your local server.


## Prerequisites:

- Make sure you have XAMPP installed on your system.
- Download and open Virtual Hosts 0.7.1 setup, which simplifies the configuration process.

## Additional Resource:
If you don’t have the Virtual Hosts 0.7.1 setup, you can download it from this link: Virtual Hosts Setup 0.7.1.[https://drive.google.com/drive/folders/1tmNrPuSztMJLvjt_f9nhej5FjNtROOiD?usp=sharing]

# Steps to Set Up Virtual Hosts:

1. Download and Open `Virtual Hosts` Setup (v0.7.1)

- Download the Virtual Hosts 0.7.1 setup from the link above if you haven't already.
- Install and open the Virtual Hosts Setup tool. This software helps simplify the process of setting up Virtual Hosts for local development in XAMPP.
- Once the tool is opened, proceed with the following steps to configure your Virtual Host settings.


## 1. Select Root Folder in XAMPP:

The root folder in XAMPP is where your website files will be stored. By default, XAMPP serves files from the **htdocs directory**.

**Steps:**

1. Navigate to the XAMPP installation directory (commonly C:\xampp on Windows).

2. Open the `htdocs folder` (this is the default web root folder).

3. Inside htdocs, create a new folder for your project (e.g., myproject). This will act as the root directory for your Virtual Host.

**Example:**
C:\xampp\htdocs\myproject

## 2. Add Localhost Configuration in `hosts File`:

- The hosts file maps domain names to IP addresses on your local machine. By adding an entry for your custom domain (e.g., myproject.example.com), you can access your project using this domain.

**Steps:**
- Open the Virtual Hosts Setup tool and navigate to the hosts file configuration section.

Alternatively, `manually` open the hosts file:

**Windows:** `C:\Windows\System32\drivers\etc\hosts`
**Linux:** `/etc/hosts`
**macOS:** `/private/etc/hosts`
Add the following entry to the hosts file:
```bash
127.0.0.1    myproject.example.com
```
- Save and close the file.

## 3. Ensure Virtual Host is Not Commented in `httpd.conf`:

The httpd.conf file in Apache controls its configuration. By default, the Virtual Hosts configuration may be disabled. You need to ensure that it is enabled.

**Steps:**
- Open the XAMPP Control Panel.

- Click Config next to Apache and select httpd.conf.

- Search for the line:

```bash
#Include conf/extra/httpd-vhosts.conf
```
- If it is commented out (with a # symbol), remove the # to uncomment it:

```bash
Include conf/extra/httpd-vhosts.conf
```
- Save and close the file.

## 4. Generate Virtual Host Code:

Each Virtual Host requires specific configuration in Apache. The Virtual Hosts Setup tool simplifies this process by generating the necessary code.

**Steps:**
- In the Virtual Hosts Setup tool, go to the Generate Virtual Host section.

Fill out the necessary fields:

**Document Root:** Path to your project folder `(C:/xampp/htdocs/myproject)`.
Server Name: Custom domain name (e.g., myproject.example.com).
The tool will generate the necessary Virtual Host code:

- The tool will generate the necessary Virtual Host code:
```bash
<VirtualHost *:80>
    ServerAdmin webmaster@myproject.example.com
    DocumentRoot "C:/xampp/htdocs/myproject"
    ServerName myproject.example.com
    ErrorLog "logs/myproject.example.com-error.log"
    CustomLog "logs/myproject.example.com-access.log" common
</VirtualHost>
```
- Copy this generated code.

## 5. Add Virtual Host in `httpd-vhosts.conf`:

- The `httpd-vhosts.conf` file contains the configuration for all Virtual Hosts.
- You need to add your Virtual Host code to this file.

**Steps:**
1. In the XAMPP Control Panel, click Config next to Apache and select httpd-vhosts.conf.

2. Scroll to the bottom of the file and paste the Virtual Host code generated in the previous step.

```bash
<VirtualHost *:80>
    ServerAdmin webmaster@myproject.example.com
    DocumentRoot "C:/xampp/htdocs/myproject"
    ServerName myproject.example.com
    ErrorLog "logs/myproject.example.com-error.log"
    CustomLog "logs/myproject.example.com-access.log" common
</VirtualHost>
```
3. Save and close the file.


## 6. Start XAMPP and Check Web Link in Browser:

Now that the Virtual Host is set up, you need to start Apache and test the configuration by accessing the custom domain in a browser.

**Steps:**
- Open the XAMPP Control Panel.
- Click Start next to Apache to start the web server.
- Open a browser and enter your custom domain `(e.g., http://myproject.example.com)`.
If everything is configured correctly, your website should load from the project folder you set up.


# Troubleshooting Tips:
**Apache Port Conflict:**
If Apache fails to start, check if another application is using port 80. You can either stop the other service or change Apache’s port in the httpd.conf file.

**Check Logs:**
Check the Apache error logs (C:\xampp\apache\logs\error.log) if you encounter issues. Logs can provide insights into misconfigurations.

**Multiple Virtual Hosts:**
If you are working on multiple projects, repeat the steps to configure additional Virtual Hosts. Each project can have its own custom domain and root folder.
