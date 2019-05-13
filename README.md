# SQL

## DATABASE
### Create Database
CREATE DATABASE ` Name of the database` CHARACTER SET utf8 COLLATE utf8_general_ci;
### Delete Database
DELETE DATABASE ` Name of the database `;
### Show Database
SHOW DATABASE;
### Use Database
USE `Name of the database`;

## TABLE
### Create Tables
CREATE TABLE table_name (
    column_name1 data_type,
    column_name2 data_type
)

ex)
CREATE TABLE `student` (
    `id`  tinyint NOT NULL ,
    `name`  char(4) NOT NULL ,
    `sex`  enum('male','female') NOT NULL ,
    `address`  varchar(50) NOT NULL ,
    `birthday`  datetime NOT NULL ,
    PRIMARY KEY (`id`)
);
### Show table list
SHOW tables;
### Show table schema(theble structure)
DESC `name of table`
### Drop the table
DROP TABLE `the name of table`
### Data Type
CHAR( ) :	put 0 to 255 of strings in (), immutable 

VARCHAR( ) : put	0~65535 of strings in (), mutable

TINYTEXT: The max length of string is 255 

TEXT: The max length of string is	65535 

BLOB	The max length of string is 65535

MEDIUMTEXT:	The max length of string is 16777215 

MEDIUMBLOB:	The max length of string is 16777215 

LONGTEXT:	The max length of string is 4294967295 

LONGBLOB:	The max length of string is 4294967295 

TINYINT( ):	-128 ~ 127 integers (SIGNED)/
0 ~ 255 integers, UNSIGNED

SMALLINT( ):-32768 ~ 32767, integers (SIGNED)/
0 ~ 65535, integers, UNSIGNED

MEDIUMINT( )	-8388608 to 8388607, integers /
0 to 16777215 , integers, UNSIGNED

INT( )	-2147483648 ~ 2147483647 integers /
0 ~ 4294967295, integers, UNSIGNED

BIGINT( )	-9223372036854775808 ~ 9223372036854775807, integers /
0 ~ 18446744073709551615, integers, UNSIGNED.

FLOAT: 작은 부동 소숫점

DOUBLE( , ) : 큰 부동 소숫점

DATE	YYYY-MM-DD.

DATETIME	YYYY-MM-DD HH:MM:SS.

TIMESTAMP	YYYYMMDDHHMMSS.

TIME	HH:MM:SS.

ENUM ( )	fixed values

SET	 

### Insert Data into Table
INSERT INTO table_name VALUES (value1, value2, value3,...)

INSERT INTO table_name (column1, column2, column3,...) VALUES (value1, value2, value3,...)

INSERT INTO `student` VALUES ('2', 'leezche', '여자', '서울', '2000-10-26');

INSERT INTO `student` (`id`, `name`, `sex`, `address`, `birthday`) VALUES ('1', 'egoing', '남자', 'seoul', '2000-11-16');


## Update Data
UPDATE table_name SET column1=new value, column2=new value WHERE index=value

UPDATE `student` SET address='seoul';

UPDATE `student` SET name='elena' WHERE id=1;

UPDATE `student` SET name='eunji', birthday='2001-4-1' WHERE id=3;

## Delete Data(delete each row of the data)
DELETE FROM 테이블명 [WHERE column=value]

DELETE FROM student WHERE id = 2;

## Truncate
### Delete all the datas in the table at once
### If there is no foreign key, this is a faster way than using 'delete' code
### It deletes all the rows without transaction but the rest of the data (such as columns, index, table structure,etc) remains
TRUNCATE table_name

TRUNCATE student;

## DROP TABLE
### 'drop' deletes the table
DROP TABLE table_name;

DROP TABLE student;
