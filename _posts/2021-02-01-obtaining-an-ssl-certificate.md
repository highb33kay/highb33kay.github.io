---
layout: post
title: "How to Obtain and Deploy an SSL Certificate for Your Website Using cPanel and acme.sh"
summary: "A guide on obtaining and deploying SSL certificates with cPanel and acme.sh"
author: highb33kay
date: "2024-01-03 1:35:23 +0530"
category: ["tutorials", "ssl-certificates", "cpanel", "acme.sh"]
tags: ssl-certificates, cpanel, acme.sh, web-security
thumbnail: /assets/img/posts/working-of-ssl.jpg
keywords: cpanel, acme.sh, ssl certificate, web security, Let's Encrypt
usemathjax: false
permalink: /blog/obtain-deploy-ssl-certificate-cpanel-acme-sh/
---

## How to Obtain and Deploy an SSL Certificate for Your Website Using cPanel and acme.sh

[acme.sh](https://acme.sh/) is a simple command-line tool for obtaining and deploying SSL certificates from Let's Encrypt. It is a popular choice for users of cPanel, as it can be easily integrated with the cPanel UAPI.

### Steps:

1. **Install acme.sh:**

   ```bash
   curl https://get.acme.sh | sh
   ```

2. **Source your .bashrc file**

   ```bash
   source ~/.bashrc
   ```

3. **Create a Let's Encrypt account**

   ```bash
   acme.sh --register-account --accountemail youremail@server.com

   ```

4. **Upgrade acme.sh:**

   ```bash
   acme.sh --upgrade
   ```

5. **Obtain a certificate for your domain:**

   ```bash
   acme.sh --register-account --accountemail youremail@server.com --server letsencrypt
   ```

6. **List your scheduled tasks to see if acme.sh is already running:**

   ```bash
   crontab -l | grep acme.sh
   ```

7. **Get the document root for your domain name from the cPanel UAPI**

   ```bash
   uapi DomainInfo single_domain_data domain=propertek.com.ng | grep documentroot
   ```

8. **Issue a Let's Encrypt SSL certificate for your domain name using acme.sh and the document root:**

   ```bash
   acme.sh --issue --webroot /home/anchtdwz/domainroot -d domain-name.com --staging
   ```

   Note: The --staging flag is optional, but it is recommended to use it first to test your SSL certificate before deploying it to production.

9. **Force acme.sh to issue a new SSL certificate, even if one already exists**

   ```bash
   acme.sh --issue --webroot /home/anchtdwz/domainroot -d domain-name.com --force
   ```

10. **Force acme.sh to issue a new SSL certificate from Let's Encrypt, even if one already exists**

    ```bash
    acme.sh --issue --webroot /home/anchtdwz/domainroot -d domain-name.com --force --server letsencrypt
    ```

11. **Deploy the SSL certificate to your cPanel server using acme.sh and the cPanel UAPI:**

    ```bash
    acme.sh --deploy --deploy-hook cpanel_uapi --domain domain-name.com
    ```

    Add the --force flag to force acme.sh to deploy the SSL certificate, even if one already exists.

### Conclusion:

acme.sh is a simple command-line tool for obtaining and deploying SSL certificates from Let's Encrypt. It is a popular choice for users of cPanel, as it can be easily integrated with the cPanel UAPI. This guide has shown you how to obtain and deploy an SSL certificate for your website using cPanel and acme.sh.
