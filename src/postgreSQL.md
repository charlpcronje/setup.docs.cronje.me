---
title: Install PostgreSQL
---
<script type="text/javascript">(function(w,s){var e=document.createElement("script");e.type="text/javascript";e.async=true;e.src="https://cdn.pagesense.io/js/webally/f2527eebee974243853bcd47b32631f4.js";var x=document.getElementsByTagName("script")[0];x.parentNode.insertBefore(e,x);})(window,"script");</script>

Run the following command to install PostgreSQL.

```sh
yum -y install postgresql-server postgresql-contrib
```

Now initialize the database using the following command.

```sh
postgresql-setup initdb
```

Start and enable PostgreSQL database service using the following command.

```sh
systemctl start postgresql
systemctl enable postgresql
```

Now run the following command to change the password of PostgreSQL root user called postgres using the following command.

```sh
sudo -u postgres psql postgres
\password postgres
```

Enter `\q` or `ctrl + D` buttons to exit Postgres shell.