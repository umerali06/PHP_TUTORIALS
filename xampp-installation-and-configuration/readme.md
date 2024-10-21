# XAMPP Installation & Run Process

## How to Run PHP Code?

To run PHP code, the following three things are required:

1. **PHP**
2. **MySQL** (or any other database that is compatible with PHP)
3. **Apache Server**

We would typically need to download and install these components separately, then configure them individually. This process can be quite lengthy, and managing each task separately is not ideal.

### Solution:
Most PHP developers use third-party software to simplify this process. Two of the most popular software solutions are:

- **WAMP**
- **XAMPP**

There are many other options, but these two are the most widely used and preferred by developers.

For our course tutorial, we will use **XAMPP**. This software includes PHP, MySQL, and Apache, and it configures them automatically during installation.

## XAMPP

**XAMPP** stands for:

- **X**: Cross-Platform
- **A**: Apache
- **M**: MySQL
- **P**: PHP
- **P**: Perl

It is an open-source software package that provides a local server environment, allowing developers to run and test web applications on their own computers.

### Why Do We Prefer XAMPP Over WAMP?

Here are the reasons why **XAMPP** is often preferred over **WAMP**, along with the limitations of the WAMP server:

- **Cross-Platform Support**: XAMPP is cross-platform and can run on **Windows, macOS, and Linux**, making it versatile for developers who work across different operating systems. WAMP is limited to **Windows only**, restricting developers to a single OS, which can be a disadvantage for cross-platform projects or developers using non-Windows environments.

- **Multiple Programming Languages**: XAMPP includes support for **PHP, Perl, and Python**, making it suitable for a variety of development environments. WAMP focuses mainly on **PHP** without built-in support for additional languages like Perl or Python, making it less flexible in that regard.

- **Pre-Configured Modules**: XAMPP comes pre-configured with several modules such as **Apache, MySQL, PHP, Perl**, and **phpMyAdmin**. It requires little manual setup, making it ready to use for development out-of-the-box. WAMP often requires more manual configuration and setup, which can be cumbersome for beginners or those who want a quick start.

## How to Install XAMPP Server

Follow these steps to install XAMPP:

1. Open your browser.
2. Visit the official XAMPP website at: [https://www.apachefriends.org](https://www.apachefriends.org)
3. Download the XAMPP setup according to your operating system.
4. Install XAMPP using the default settings.
   - By default, it will be installed in `C:/xampp`.

After installation, you can begin running PHP code and testing your web applications in the local environment provided by XAMPP.

---

**Note**: Once installed, XAMPP provides you with everything you need to develop and test PHP applications locally, including a MySQL database, Apache server, and the necessary configurations to get started quickly.

After the Installation of the setup , we need to Modify the Virtual host Configuration.

## What is Virtual Hosts Configuration?

Virtual Hosts allow you to run **multiple websites** on the **same server**, even if the server has only **one IP address**. This is achieved by assigning different ServerName values (like localhost or test.localhost), which allows the server to differentiate between different web applications or projects.


## Why Modify Virtual Hosts Configuration in XAMPP?

By default, XAMPP points all requests to a single folder (htdocs) inside the XAMPP directory. This may not be efficient if you want to work on multiple projects simultaneously. Modifying the Virtual Hosts configuration enables you to:

- **Run multiple projects:** 
You can assign different domain names to different projects, making it easier to access them.

- **Mimic real hosting environments:**
This allows you to simulate how websites would function on live servers with different domain names.

- **Organize projects:**
Rather than placing all projects inside a single htdocs folder, you can assign different folders for each project.

## Virtual Hosts Configuration :

```bash
<VirtualHost *:80>
    DocumentRoot "C:/xampp/htdocs/"
    ServerName localhost
</VirtualHost>

<VirtualHost *:80>
    DocumentRoot "C:/xampp/htdocs/test"
    ServerName test.localhost
</VirtualHost>
```

## Explaination of the Configuration:

**a. <VirtualHost *:80>:**
This defines a Virtual Host that listens on **port 80** (the default HTTP port) for incoming requests. The *** symbol** means that it will listen on any IP address.

**b. DocumentRoot**
DocumentRoot **"C:/xampp/htdocs/":** This line specifies the folder from which Apache should serve files when you access localhost (the default domain).
DocumentRoot "C:/xampp/htdocs/test": This line points to the folder where the project for the domain test.localhost resides.
This means that when you visit **test.localhost**, XAMPP will serve the files from the **test folder** inside the **htdocs directory**, simulating a separate website.

**c. ServerName**
ServerName localhost: This tells Apache to serve the default localhost domain, pointing to htdocs/.
ServerName test.localhost: This configures another domain called test.localhost, which Apache will recognize as a different website, served from the htdocs/test folder.

## Why Do You Need This Modification?

There are several important reasons for modifying Virtual Hosts:

1. **Host Multiple Websites Locally**

By default, XAMPP only provides access to the root folder (htdocs) via localhost. If you are working on multiple projects, modifying Virtual Hosts allows you to assign unique URLs for each project (e.g., project1.localhost, project2.localhost).

2. **Organize Development Projects**

You can organize projects into their respective folders and access each via a dedicated local domain name. For example:

- Main project at localhost
- Subproject at test.localhost

This keeps your development environment clean and prevents file clutter in a single htdocs folder.

3. **Better Testing and Debugging**

Having multiple projects configured with separate domain names helps you test and debug each project in isolation. This makes it easier to work with different projects simultaneously without mixing configurations or files.


## How to Apply the Virtual Hosts Configuration in XAMPP?

**Step 1:** 
Open the Virtual Hosts Configuration File
Navigate to C:/xampp/apache/conf/extra/
Open the file httpd-vhosts.conf

**Step 2:** 
Modify the File
Add the following code at the end of the file to set up the localhost and test.localhost domains:

```bash
<VirtualHost *:80>
    DocumentRoot "C:/xampp/htdocs/"
    ServerName localhost
</VirtualHost>

<VirtualHost *:80>
    DocumentRoot "C:/xampp/htdocs/test"
    ServerName test.localhost
</VirtualHost>
```

**Step 3:** 
Edit Your hosts File
You need to map your custom domains (test.localhost) to the local machine (127.0.0.1). To do this:

Open C:/Windows/System32/drivers/etc/hosts (in Notepad as Administrator).
Add the following lines at the bottom of the file:

```bash
127.0.0.1 localhost
127.0.0.1 test.localhost
```

This tells your computer that localhost and test.localhost should resolve to 127.0.0.1 (your local machine).


**Step 4:**
 Restart Apache Server
After making changes to the configuration, restart Apache from the XAMPP control panel to apply the changes.