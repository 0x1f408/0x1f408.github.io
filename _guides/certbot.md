##Install Certbot:

### Overview:

Certbot is an open source utility maintained by EFF, to generate \[free\] SSL certificates via [LetsEncrypt](https://letsencrypt.org/), written in Python.

For this tutorial, we will be working on Debian 9, release name `stretch`; for other versions (e.g.: Debian 7/8), 
replace `stretch` with the appropriate release name (e.g.: `wheezy`, `jessie`).

For other directions, see Certbot's [official installation instructions]().

You will need to do this after installing and configuring [JIRA]().

### Instructions:
<!-- todo: add descriptions for each of these sections (e.g.: what it does, why you're doing it -->

1. \[[link](https://backports.debian.org/Instructions/)\] Add `stretch-backports` to your `sources.list`: 
    ```sh 
    sudo echo 'deb http://ftp.debian.org/debian stretch-backports main' >> /etc/apt/sources.list
    ```
    *Make sure that you use `>>`, not `>`; the second will overwrite your `sources.list`*.

2. \[[link](https://certbot.eff.org/lets-encrypt/debianstretch-apache)\] Install Certbot:
    ```sh 
    sudo apt-get install python-certbot-apache -t stretch-backports
    ```

### Note: we'll need to reconfigure the below steps, as JIRA has a different setup from most webapplications
It's installed to /var/atlassian/application-data/jira by default

3. Create your web application directory.
    ```sh 
    sudo -u www-data mkdir /var/www/trms
    ```  
4. Create a symbolic link to your JIRA installation.
    ```sh
    sudo -u www-data ln -s /var/www/trms /usr/lib/atlassian-jira-software-7.9.1-standalone/webapps/trms
    ```
 5. Create certificate, via Certbot (finally).
    ```sh
    sudo certbot certonly --webroot -w /path/to/tomcat/webapps -d $YOURDOMAIN -d jira.$YOURDOMAIN
    ```
    
    Substitute your domain, e.g.: example.com, in place of $YOURDOMAIN. 
    You may add additional subdomains (e.g.: jira, www) by adding `-d $SUBDOMAIN.$YOURDOMAIN`.
    
    For example, the command I used was: 
    
    ```sh
    sudo certbot certonly --webroot -w /var/www/trms -d jira.0x1f408.me
    ```