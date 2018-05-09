---
layout: post
permalink: /guide/aws
title: Amazon Web Services - RDS
subtitle: Quick overview of Relational Database Services on AWS
---
## AWS RDS

AWS provides a much better guide than I can, which can be found [here](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_SettingUp.html).
Below is a [very] rough overview.

## Rough instructions

#### 1. Register an account on [AWS](https://aws.amazon.com/). 

This will be your root user for all AWS services. Note that this will be free for the first twelve (12) months, 
after which the price increases to **$29/month**.

#### 2. Enable MFA

If you don't have a hardware key, Google Authenticator or Authy TFA are supported.
Scan the provided code and enter two (2) consecutive codes.

#### 3. Create an IAM user

This will be the user account that actually manages the RDS, for security reasons. 
Create an `Administrators` group, and assign it `AdministratorAccess`.

#### 4. Configure the RDS instance

Unless you're using an E2 instance, you will need to make this publicly accessible. 
We'll configure who can access it in a bit.

#### 5. Define a root (master) user & assign it a password. 

These will be your login credentials for the RDS instance itself.

#### 6. `Launch` the instance. 

It will take some time to load, and will back up immediately initial creation. Once it's avaiable,
log in to the provided address using the master user you defined previously, from an SQL client of your choice.

**Reorganize the below**
Add whitelisted IPs: Create a group and add rules to it to allow access.
Here, I whitelisted the Appian instance, and the VPS running JIRA.

https://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_SecurityGroups.html#AddRemoveRules

## Create security groups (enable access to RDS)

#### 1. Navigate to `Security Groups`, under *Security* on the left navigation bar.

#### 2. Create a new Security group
 
Create a new group, using the `Create Security Group` button (top left). 
Assign it a name, a group, and a description, and assign it to your VPC.

#### 3. Edit the new group

Select the new group, and select the `Inbound Rules` tab from the Edit Group section below.

#### 4. Add your whitelisted IPs or ranges.

After selecting your group, click `Edit`. Enter into the fields in the lower table:

    * Type: The type of connection (MySQL/Aurora(3306))
    * Protocol: The protocol to whitelist (TCP(6))
    * Port: The port to whitelist (for MySQL, 3306)
    * Range: An IP range and prefix (e.g.: /24). `0.0.0.0/0` will whitelist all IPs.
    * Description: A brief description of the specified range

#### 5. Save.

#### 6. Assign the new security groups to your instance

1. Navigate back to your RDS instance's dashboard, and select `Modify` from under the `Instance Actions` dropdown (top right).

1. Under `Network and Security`, select the Security Group you just created from under the `Security Group` dropdown.

1. Click `Continue`, then select `Apply Immediately` (if you don't want to wait until your next specified 

1. maintenance window). Click `Modify DB Instance`. The RDS instance should reboot at this time, to apply changes.

## Follow-up

#### 1. If you have an existing domain, redirect a subdomain to point to your RDS instance

Log into your domain provider, or CloudFlare, depending on where the name resolution for your domain is set up.
Create a new **CNAME** record, pointing db.`$yourdomain` to the domain provided on the dashboard for your RDS instance.

    * This isn't *required*, but remembering `db.0x1f408.me` is a lot easier than remembering 
`trms-va-01.$randomstring.us.east-1.rds.amazon.com`.

#### 2. Log into the RDS instance from a MySQL client of your choice

If on Windows, the CLI client is finnicky, but MySQL Workbench gets the job done here. 

    * If on *nix, use:
    ```
    mysql -u $username -p -h $domain
    ```
    e.g.: `mysql -u kit -p -h db.0x1f408.me`

#### 3. Create databases
    
    ```mysql
    CREATE DATABASE trms;
    CREATE DATABASE jira;
    ```
    
#### 4. Create new user(s) and assign them passwords.

    ```mysql
    GRANT ALL ON 'trms'.* TO 'trms-user'@'$domain' IDENTIFIED BY '$unique_password';
    GRANT ALL ON 'jira'.* TO 'jira-user'@'$domain' IDENTIFIED BY ' $unique_password';
    ```
    
    Note that `$domain` here refers to the domain you will be accessing this from (e.g.: jira.0x1f408.me), and
    **not** the domain of the database itself. The created users will only be able to access the database from this domain;
    however, the wildcard `%` is accepted.

    For example: `GRANT ALL ON 'jira'.* TO 'jira-user'@'%.0x1f408.me' IDENTIFIED BY 'thisisaverybasicpassword`

    The [MySQL Documentation](https://dev.mysql.com/doc/refman/5.7/en/grant.html) provides a much more in-depth view,
    including per-column permissions, authentication, and more.