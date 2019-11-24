---
layout: post
title: Reset root password for mysql
tags: [mysql]
---

Sometimes I totally forgot the root password that I set for `mysql`. So, I'm writing these steps for my own reference, and for others who faced the same problem.

## Steps

Firstly, **stop** `mysql` service and then **start** `mysql` service with the `--skip-grant-tables` option:

```shell
sudo service mysql stop
sudo mysqld --skip-grant-tables
mysql -u root mysql
```

Update the root password with the new password:

```shell
UPDATE user SET password = PASSWORD('newpass')
WHERE user = 'root';
FLUSH PRIVILEGES;
```

Finally, restart `mysql` service normally:

```shell
sudo service mysql restart
```

Now you should be able to login `mysql` as root with the new password.

```shell
mysql -u root -p
```
