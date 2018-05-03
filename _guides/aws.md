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

1. Register an account on [AWS](https://aws.amazon.com/). This will be your root user for all AWS services.
Note that this will be free for the first twelve (12) months, after which the price increases to $29/month.

2. Enable MFA - if you don't have a hardware key, Google Authenticator or Authy TFA are supported.
Scan the provided code and enter two (2) consecutive codes.

3. Create an IAM user; this will be the user account that actually manages the RDS, for security reasons. 
Create an `Administrators` group, and assign it `AdministratorAccess`.

4. Configure the RDS instance; unless you're using an E2 instance, you will need to make this publicly accessible. 

5. Define a root (master) user and assign it a password. These will be your login credentials for the RDS instance itself.

6. `Launch` the instance. It will take some time to load, and will back up immediately initial creation. Once it's avaiable,
log in to the provided address using the master user you defined previously, from an SQL client of your choice.

## Follow-up

1. Log into your domain provider, or CloudFlare, depending on where the name resolution for your domain is set up.
Create a new **CNAME** record, pointing db.`$yourdomain` to the domain provided on the dashboard for your RDS instance.

    * This isn't *required*, but remembering `db.0x1f408.me` is a lot easier than remembering 
`trms-va-01.$randomstring.us.east-1.rds.amazon.com`.

2. Log into the RDS instance from a MySQL client of your choice - if on Windows, the CLI client is finnicky, 
but MySQL Workbench gets the job done here. 

    * If on *nix, use:
    ```
    mysql -u $username -p -h $domain
    ```
    e.g.: `mysql -u kit -p -h db.0x1f408.me`

3. Create databases
    
    ```mysql
    CREATE DATABASE trms;
    CREATE DATABASE jira;
    ```
4. Create new user(s) and assign them passwords.

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