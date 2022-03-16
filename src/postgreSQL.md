# Install PostgreSQL

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