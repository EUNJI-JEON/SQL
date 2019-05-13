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

## SELECT
### SELECT FROM
SELECT * FROM student;

SELECT name, birthday FROM student;

### SELECT WHERE + AND/OR
SELECT * FROM student WHERE id=3;

SELECT * FROM student WHERE sex='남자' AND address='서울';

SELECT * FROM student WHERE sex='여자' OR address='서울';

### SELECT LIMIT (limit the length of the data)

SELECT * FROM student LIMIT 1;

SELECT * FROM student WHERE sex='male' LIMIT 2;

### LIMIT + {start index(count from 0), length(number) of data} : 
SELECT * FROM student LIMIT 1,1; 

SELECT * FROM student LIMIT 2,1;

SELECT * FROM student LIMIT 3,1;


## Group By
SELECT * FROM table_name GROUP BY a column for grouping

select gender from student group by gender;

select gender,sum(distance), avg(distance) from student group by gender;

## Order
### desc(descendent) : reverse order(e.g. latest order, from biggest) of data (<-> asc(ascendent)) 
SELECT * FROM table_name ORDER BY a standard column for order [DESC | ASC]

select * from student order by distance desc;

select * from student order by distance asc;


## Index
### primary key
#### 테이블 전체를 통틀어서 중복되지 않는 값을 지정해야 한다.
#### where 문을 이용해서 데이터를 조회할 때 가장 고속으로 데이터를 가져올 수 있다.
#### 테이블마다 딱 하나의 primary key를 가질 수 있다.
select * from student where id=3;

### Unique key
#### 테이블 전체를 통틀어서 중복되지 않는 값을 지정해야 한다. (== primary key)
#### 고속으로 데이터를 가져올 수 있다.
#### 여러개의 unique key를 지정할 수 있다.
select * from student where number=0534543;

### Normal key
#### 중복을 허용한다.
#### primary, unique 보다 속도가 느리다.
#### 여러개의 키를 지정할 수 있다.
select * from student where department='Business'

### Full Text
#### mysql의 기본설정(ft_min_word_len)이 4로 되어 있기 때문에 최소 4글자 이상을 입력하거나 이 값을 조정해야 한다.
#### mysql은 전문 검색 엔진이 아니기 때문에 한글 검색이 잘 안된다.
#### 전문검색엔진으로 lucene, sphinx 참고
#### 스토리지 엔진 중 myisam에서만 사용가능
#### AGAINST('매치할 값')
SELECT introduction, MATCH(introduction) AGAINST('major in Business') FROM student WHERE MATCH (introduction) AGAINST('major in Business');

### Overlapping key
#### 하나의 키에 여러개의 칼럼을 포함
select * from student where department='Business' AND address='Jeju';

## Join
### Join Types
#### Outer Join & Inner Join
##### OUTTER JOIN : 매칭되는 행이 없어도 결과를 가져오고 매칭되는 행이 없는 경우 NULL로 표시한다. LEFT JOIN과 RIGHT JOIN이 있다.
##### INNER JOIN : 조인하는 두개의 테이블 모두에 데이터가 존재하는 행에 대해서만 결과를 가져온다.
SELECT s.name, s.location_id, l.name AS address, l.distance  FROM student AS s LEFT JOIN location AS l ON s.location_id = l.id;
SELECT s.name, s.location_id, l.name AS address, l.distance  FROM student AS s INNER JOIN location AS l ON s.location_id = l.id;

![1861](./image/1861.png)
#### Left Join
SELECT s.name, s.location_id, l.name AS address, l.distance  FROM student AS s LEFT JOIN location AS l ON s.location_id = l.id;

