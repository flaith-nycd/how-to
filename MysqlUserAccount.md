# MySQL user accounts

## Get a list of user accounts
```
SELECT User FROM mysql.user;
```

## Show GRANTs for all users
```
SHOW GRANTS;

SHOW GRANTS FOR <username>;
```

Or

```
SELECT * from information_schema.user_privileges;
```

## Reset my MySQL password from [Help Ubuntu](https://help.ubuntu.com/community/MysqlPasswordReset)
To reset your mysqld password just follow these instructions :

1. Stop the mysql demon process using this command :
   ```
   sudo /etc/init.d/mysql stop
   ```
2. Start the mysqld demon process using the --skip-grant-tables option with this command 
   ```
   sudo /usr/sbin/mysqld --skip-grant-tables --skip-networking &
   ```
__Because you are not checking user privs at this point, it's safest to disable networking. In Dapper, /usr/bin/mysqld... did not work. However, mysqld --skip-grant-tables did.__

1. Start the mysql client process using this command 
   ```
   mysql -u root
   ```
2. From the mysql prompt execute this command to be able to change any password
   ```
   FLUSH PRIVILEGES;
   ```
3. Then reset/update your password 
   ```
   SET PASSWORD FOR root@'localhost' = PASSWORD('password');
   ```
4. If you have a mysql root account that can connect from everywhere, you should also do:
   ```
   UPDATE mysql.user SET Password=PASSWORD('newpwd') WHERE User='root';
   ```
5. Alternate Method:
   ```
   USE mysql
   UPDATE user SET Password = PASSWORD('newpwd')
   WHERE Host = 'localhost' AND User = 'root';
   ```
6. And if you have a root account that can access from everywhere:
   ```
   USE mysql
   UPDATE user SET Password = PASSWORD('newpwd')
   WHERE Host = '%' AND User = 'root';
   ```
For either method, once have received a message indicating a successful query (one or more rows affected), flush privileges:
```
FLUSH PRIVILEGES;
```
Then stop the mysqld process and relaunch it with the classical way:
```
sudo /etc/init.d/mysql stop
sudo /etc/init.d/mysql start
```
