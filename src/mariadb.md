---
title: Install MariaDB on CentOS 7
---
<script type="text/javascript">(function(w,s){var e=document.createElement("script");e.type="text/javascript";e.async=true;e.src="https://cdn.pagesense.io/js/webally/f2527eebee974243853bcd47b32631f4.js";var x=document.getElementsByTagName("script")[0];x.parentNode.insertBefore(e,x);})(window,"script");</script>

## Benefits of MariaDB Server 10.4

While CentOS 7 and RHEL 7 include MariaDB Server 5.5, substantial improvements have been made as MariaDB Community Server changed through the 10.0, 10.1, 10.2, 10.3, and 10.4 release series. The MariaDB Server 10.4 release series includes:

- Instant `ALTER` for `InnoDB` tables
- Optimizer trace to aid in performance diagnosis
- Window functions and Common Table Expressions (CTE)
- `Temporal` tables, including system-versioned, application time-period, and `bitemporal` (both)
- Ability to reload `SSL certificates` without server restart
- `Galera 4` technology, a major enhancement over `Galera 3`
- Additional storage engines, including `MyRocks`
- `SQL_MODE`=`ORACLE` for compatibility with a subset of `Oracle PL/SQL`
- Expanded `data-at-rest` encryption
- Authentication enhancements, including multiple authentication methods per user

## To install MariaDB and dependencies

```shell
sudo yum install mariadb-server
```

## Configuring and Securing MariaDB Server

Start the systemd service for `MariaDB Server 5.5` or `10.4` using systemctl:

```shell
sudo systemctl start mariadb.service
```

Specific security practices should always follow any business-specific requirements and governance. Some basic steps should be taken to help harden the `MariaDB Community Server 5.5` or `10.4 deployment`:

```shell
sudo mysql_secure_installation
```
