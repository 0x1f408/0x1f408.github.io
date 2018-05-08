---
layout: post
permalink: /guide/jira
title: Atlassian JIRA
subtitle: Creating your first project on JIRA
---

1. [link](https://confluence.atlassian.com/adminjiraserver073/connecting-jira-applications-to-mysql-861253043.html) Configure JIRA to use the database you previously created.

2. Copy the Connector/J .jar to <jira install location>/lib
  ```sh 
  mv ~/mysql-connector-java-8.0.9-rc.jar /usr/lib/atlassian-jira-software-7.9.1-standalone/lib
  ```
  Note that the first location (`~/mysql...jar`) is the initial file location, and `/usr/lib/.../lib` is the
  JIRA install location. Depending on your setup, these may vary.
  
3.  