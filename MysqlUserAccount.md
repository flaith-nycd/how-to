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
