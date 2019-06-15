# Replication test between MariaDB and Mysql

## Preparation on master
CREATE USER 'repl_user'@'%';

GRANT REPLICATION SLAVE ON *.* TO 'repl_user'@'%' IDENTIFIED BY 'pass';

show master status;

--> Use result value for LOG_FILE and LOG_POS

## Preparation on slave
`GRANT REPLICATION_SLAVE_ADMIN, GROUP_REPLICATION_ADMIN, BINLOG_ADMIN ON *.* TO 'root'@'%'

CHANGE MASTER TO MASTER_HOST='master',
  MASTER_USER='repl_user',
  MASTER_PASSWORD='pass',
  MASTER_LOG_FILE='mysql-bin.000004',
  MASTER_LOG_POS=342;

start slave;`