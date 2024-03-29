---
title: DB Connectors
label: Server & Software Setup
order: 100
authors:
  - name: Charl Cronje
    email: charl@CRONje.ME
    link: https://blog.cronje.me
    avatar: https://assets.cronje.me/avatars/darker.jpg
edit:
  repo: "https://github.com/charlpcronje/setup.docs.devserv.me/edit/"
  base: /src
  branch: main
  label: Edit on GitHub
editor:
  enabled: false
favicon: favicon.png
links:
- text: Dashboard
  link: https://nav.cronje.me
- text: Blog / Portfolio
  link: https://blog.cronje.me
- text: Wiki, Tips and Docs 
  link: https://docs.cronje.me
- text: My CV
  link: https://cv.cronje.me
- text: LinkedIn
  link: https://www.linkedin.com/in/charlpcronje
- text: GitHub
  link: https://github.com/charlpcronje
- text: Upwork Profile
  link: https://www.upwork.com/freelancers/~01ccb1439024ec9c50
footer:
  copyright: "webAlly &copy; Copyright {{ year }}. All rights reserved."
---
<script type="text/javascript">(function(w,s){var e=document.createElement("script");e.type="text/javascript";e.async=true;e.src="https://cdn.pagesense.io/js/webally/f2527eebee974243853bcd47b32631f4.js";var x=document.getElementsByTagName("script")[0];x.parentNode.insertBefore(e,x);})(window,"script");</script>


> Here is a list of connectors for `Maria DB` on most platforms and use cases. The `ODBC Connection` is the fastest and easiest to install for Windows.

You can check which `ODBC` connections:

1. Has already been setup in Windows by shortcut `[Start Button]` 
2. Type `ODBC Data Sources`

## Download Links

- [C Connector](https://downloads.mariadb.com/Connectors/c/)
- [CPP Connector](https://downloads.mariadb.com/Connectors/cpp/)
- [Java Connector](https://downloads.mariadb.com/Connectors/java/)
- [NodeJS](https://downloads.mariadb.com/Connectors/nodejs/)
- [ODBC Connector](https://downloads.mariadb.com/Connectors/odbc/lates/)
- [PowerBI Connector](https://downloads.mariadb.com/Connectors/powerbi-adapter/)
- [Python Connector](https://downloads.mariadb.com/Connectors/python/)
- [r2dbc Connector](https://downloads.mariadb.com/Connectors/r2dbc/)

## Adding ODBC Connection Windows

> To open the ODBC Data Source Administrator in Windows 10
On the `Start page`, type `ODBC Data Sources`. The `ODBC Data Sources Desktop App` should appear as a choice.

> To open the ODBC Data Source Administrator in Windows 7

- On the `Start menu`, click `Control Panel`.
- In `Control Panel`, click `Administrative Tools`.
- In `Administrative Tools`, click `Data Sources (ODBC)`.

To open the `ODBC Data Source Administrator` in `Windows Server 2008`
On the `Start menu`, point to `Administrative Tools`, and then `click Data Sources (ODBC)`.
 Note

For connections to `Azure Active Directory Authentication` for `SQL Database install` the latest driver, such as `ODBC Driver 17 for SQL Server`

## See Also

[Check the ODBC SQL Server Driver Version Windows](https://docs.microsoft.com/en-us/sql/database-engine/configure-windows/check-the-odbc-sql-server-driver-version-windows?view=sql-server-ver15)
