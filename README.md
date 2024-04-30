## Schedule Management Database Project Demo
![alt text](https://github.com/tamim2007009/Schedule-Management/blob/main/Assets/Capture.PNG)

## Download Oracle database
> Download the  ([Oracle Database 11g Express Edition](https://www.oracle.com/database/technologies/xe-prior-release-downloads.html)) and install the software.
>> Remember the password during the installation because this password is used for connecting the database account.
![alt text](https://github.com/tamim2007009/Schedule-Management/blob/main/Assets/installation.png)

> Open the SQL Plus. Write 'connect system' and use the password that you set in the installation process. Follow the below figure.

```
connect system;
```

```
connect / as sysdba
alter user system identified by [password]
```

## Creating user and giving system privileges

```
create user tamim identified by [password];
```
##For deleting any user;
```
drop user username;
```
>
>
```
drop user [username] cascade;
```
>>This will drop the  user along with all objects owned by it.

>  Granting system privileges
```
grant all privileges to tamim;
```
> Reboke all the privileges from the user
```
revoke all privileges from user_name
```
>> Now disconnect the system and connect the user;
```
disconnect;
```
```
connect tamim;
```
 Now see the user with system password
```
show user;
```
## Set line size and page size
```
show pagesize
show linesize
```
```
set pagesize 400
set linesize 400
```
## Run the SQL command
> You can run SQL script by using the SQL command line. Besides, you can write your SQL command in a txt file and save the txt file as a SQL extension. Then, type the below command in the SQL command line.
```
start C:\Users\Tamim\Desktop\file1.sql
```

## Checking the existing table in database.
```
select table_name from user_tables;
```
# DDL
## Create a dummy table
```
create table dummy(
    id varchar(20),
    primary key(id)
);
```
## Add a new column
```
alter table dummy add address varchar(20);
```
## Modify the column name
```
alter table dummy  rename column address to user_name;
```
## Modify column definition
```
alter table dummy  modify user_name varchar(50);
```
## Show table
```
describe dummy;
```

![alt text](https://github.com/tamim2007009/Schedule-Management/blob/main/Assets/describe.PNG)


## Drop table column
```
alter table dummy drop column user_name;
```
## Drop table
```
drop table dummy;
```

# Creating all tables for Schedule Management project
## user_table
```
create table user_table(
	user_id varchar(50) primary key,
	name varchar(30),
	email varchar(30) not null,
	password varchar(20) not null
);
```
## day_schedule
```
 CREATE TABLE day_schedule(
       event_date VARCHAR(10) PRIMARY KEY,
        day VARCHAR(10),
        uploader VARCHAR(30),
       upload_time VARCHAR(20),
        user_id VARCHAR(50) not null,
       FOREIGN KEY (user_id) REFERENCES user_table(user_id)
    );

```

## time_schedule
```
CREATE TABLE time_schedule(
    task_id INTEGER,
    message VARCHAR(50), 
    is_completed INTEGER,
    time varchar(20),
    event_date VARCHAR(10),
    FOREIGN KEY (event_date) REFERENCES day_schedule(event_date),
    PRIMARY KEY (task_id)
);
```
## Notification
```
CREATE TABLE notification(
        task_id INTEGER,
        user_id VARCHAR(50),
        message_new VARCHAR(50),
       is_completed INTEGER CHECK (is_completed IN (0,1)),
        FOREIGN KEY (user_id) REFERENCES user_table(user_id),
        FOREIGN KEY (task_id) REFERENCES time_schedule(task_id),
       PRIMARY KEY (user_id, task_id)
    );
```
![alt text](https://github.com/tamim2007009/Schedule-Management/blob/main/Assets/tables.PNG)

# DML
## insert the data in tables
```
insert into user_table(user_id,name,email,password) values('2007001','Peyal','peyal@gmail.com','peyal');

insert into user_table values('2007002','Ebrahim','ebrahim@gmail.com','ebrahim');

insert into user_table values('2007003','Argha','argha@gmail.com','argha');
insert into user_table values('2007004','Polok','polok@gmail.com','polok');
insert into user_table values('2007005','Raihan','Raihan@gmail.com','raihan');

insert into user_table values('2007006','Omayer','omayer@gmail.com','omayer');
insert into user_table values('2007007','Shakib','shakib@gmail.com','shakib');
insert into user_table values('2007008','Ryad','ryad@gmail.com','ryad');
insert into user_table values('2007009','Tamim','tamim@gmail.com','tamim');
insert into user_table values('2007010','Sefat','sefat@gmail.com','sefat');
```
```


insert into day_schedule(event_date,day,uploader,upload_time,user_id) 
values('23/04/2024','Tuesday','Peyal','23 April at 12:50PM','2007001');

insert into day_schedule(event_date,day,uploader,upload_time,user_id) values('24/04/2024','Wednesday','Ebrahim','24 April at 12:50AM','2007002');

insert into day_schedule(event_date,day,uploader,upload_time,user_id) 
values('26/04/2024','Friday','Polok','26 April at 12:50PM','2007004');

insert into day_schedule(event_date,day,uploader,upload_time,user_id) 
values('27/04/2024','Satarday','Raihan','27 April at 12:00AM','2007005');

insert into day_schedule(event_date,day,uploader,upload_time,user_id) 
values('28/04/2024','Sunday','Omayer','28 April at 12:50PM','2007006');

insert into day_schedule(event_date,day,uploader,upload_time,user_id) 
values('29/04/2024','Monday','Shakib','29 April at 12:50PM','2007007');

insert into day_schedule(event_date,day,uploader,upload_time,user_id) 
values('30/04/2024','Tuesday','Ryad','30 April at 12:50PM','2007008');

insert into day_schedule(event_date,day,uploader,upload_time,user_id) 
values('01/05/2024','Wednesday','Tamim','01 May at 12:50PM','2007009');

insert into day_schedule(event_date,day,uploader,upload_time,user_id) 
values('02/05/2024','Thursday','Sifat','05 May at 12:50PM','2007010');
```
```
insert into time_schedule(task_id,message,is_completed,time,event_date) 
values(200,'Renew library book', 0,'10:00AM','23/04/2024');

insert into time_schedule values (201,'Have to go office', 1,'08:00AM','24/04/2024');

INSERT INTO time_schedule VALUES (202,'Prepare presentation', 1,'10:00AM', '26/04/2024');

INSERT INTO time_schedule VALUES (210,'Read a book', 1,'04:00PM', '27/04/2024');

INSERT INTO time_schedule VALUES (203, 'Attend project meeting', 0,'02:30PM','28/04/2024');

INSERT INTO time_schedule VALUES (204, 'Client meeting',1,'07:30PM', '29/04/2024');

INSERT INTO time_schedule VALUES (205,'Prepare for exam', 0,'05:00AM', '30/04/2024');

INSERT INTO time_schedule VALUES (206,'Workout at the gym', 1,'05:00PM', '01/05/2024');

INSERT INTO time_schedule VALUES (207, 'Research new technology', 0,'09:00AM', '02/05/2024');

INSERT INTO time_schedule VALUES (208, 'Lunch with colleagues',  1,'02:00PM', '01/05/2024');

INSERT INTO time_schedule VALUES (209, 'Submit project report', 1,'10:PM','24/04/2024');


INSERT INTO time_schedule VALUES (111, 'Pay bills',1,'08:00PM', '26/04/2024');
INSERT INTO time_schedule VALUES (112, 'Meeting with team', 0,'9:00PM', '30/04/2024');
INSERT INTO time_schedule VALUES (113, 'Submit expense report', 1, '10:00PM','29/04/2024');
INSERT INTO time_schedule VALUES (114,'Team dinner', 1,'8:50PM', '02/05/2024');
```

```
INSERT INTO notification (task_id, user_id, message_new, is_completed)
VALUES (201, '2007002', 'You have successfully attended the office today.', 1);

INSERT INTO notification VALUES (200, '2007001', 
'You need to renew your library book by 10:00AM ', 0);

INSERT INTO notification (task_id, user_id, message_new, is_completed)
VALUES (202, '2007003', 'Your presentation is completed.', 1);


INSERT INTO notification (task_id, user_id, message_new, is_completed)
VALUES (210, '2007004', 'You have completed reading a book.', 1);

INSERT INTO notification (task_id, user_id, message_new, is_completed)
VALUES (203, '2007005', 'You have an upcoming project meeting at 02:30PM', 0);


INSERT INTO notification (task_id, user_id, message_new, is_completed)
VALUES (204, '2007006', 'You have a client meeting scheduled at 07:30PM ', 1);


INSERT INTO notification (task_id, user_id, message_new, is_completed)
VALUES (208, '2007009', 'You have a lunch with colleagues at 02:00PM .', 1);

INSERT INTO notification (task_id, user_id, message_new, is_completed)
VALUES (207, '2007010', 'You need to research on new technology.', 0);


```
![alt text](https://github.com/tamim2007009/Schedule-Management/blob/main/Assets/data1.PNG)
![alt text](https://github.com/tamim2007009/Schedule-Management/blob/main/Assets/data2.PNG)

## Displaying table using SELECT command
```
select * from user_table where user_id =2007009;
```
```
select * from user_table where user_id >2007001 and user_id <2007009;
```
Nested select and project command
```
select * from user_table where user_id =(select user_id from day_schedule where uploader='Tamim');
```
## Update data in a table
```
update time_schedule set time ='10:00 PM' where task_id=209;
```

## Deleting row from a table
```
 delete from time_schedule where task_id=113;
```
# union, intersect, and except

```
SELECT user_id FROM user_table
UNION
SELECT user_id FROM day_schedule;

```
This query will return a list of all unique user_ids from both tables, effectively combining the two lists and removing any duplicates.

```
SELECT user_id FROM user_table
INTERSECT
SELECT user_id FROM day_schedule;

```
This query will return only the user_ids that are common to both tables.

```

SELECT user_id FROM user_table
MINUS
SELECT user_id FROM day_schedule;

```
This query will return the user_ids that are present in the user_table but not in the day_schedule table.

```
SELECT *
FROM user_table
MINUS
SELECT *
FROM user_table
WHERE user_id IN ('2007001', '2007002', '2007003');

```

## With clause
```
WITH excluded_users AS (
    SELECT *
    FROM user_table
    WHERE user_id NOT IN ('2007001', '2007002', '2007003')
)
SELECT *
FROM excluded_users;

```
 defining a table named excluded_users that selects all users except those with user IDs '2007001', '2007002', and '2007003'.


# Save the SQL command output
## Save the SQL command output in CSV file
> Simply change the folder path and your sql command.
```
SET COLSEP ","
SET HEADING OFF
SET PAGESIZE 0
SET FEEDBACK OFF
SPOOL C:\Users\Tamim\Desktop\file1.sql
SELECT *
FROM user_table;
SPOOL OFF

```
## Save the SQL command output in txt file
> Simply change the folder path and your sql command.
```
SPOOL C:\Users\Tamim\Desktop\file2.sql
SELECT *
FROM time_schedule;
SPOOL OFF
```
## Aggregate function
We count how many row exist in dept table.
```
select count(*) from user_table;
 ```

 We also give alias name to any output in select command.
 ```
select count(dept_name) as number_of_dept from dept;
 ```
We can count distinct uploader name in day_schedule.
 ```
select count(distinct uploader) as users from day_schedule;
 ```
We can count average and total task in notification.
 ```
select avg(task_id) from notification;
select sum(task_id) from notification;
 ```
We can find max and min task_id of any notification from notification table.
 ```
 select max(task_id) from notification;
 select min(task_id) from notification;
```
## Order by clause
```
select * from day_schedule order by upload_time;
```
This will show data in ascending(by default) order base on order by condition
```
select * from user_table order by name desc;
```
# Group by and Having
```
select is_completed,count(*) from notification group by is_completed;
```
This command will find no of task completed and not completed
```
 select day,count(*) from day_schedule group by day;
```
Adding HAVING after that
```
 select day,count(*) from day_schedule group by day having count(*)>1;
```

The WHERE clause places conditions on the selected columns , whereas the HAVING clause places conditions on groups created by the GROUP BY clause



# PL/SQL
## PL/SQL variable declaration and print value
```
set serveroutput on
declare
    id user_table.user_id%type;
    name user_table.name%type;
    email user_table.email%type;
    password user_table.password%type; 
begin
    select user_id, name, email, password
    into id, name, email, password
    from user_table
    where user_id = '2007009'; 
    
    dbms_output.put_line('ID: '||id|| ' Name: '||name || ' Email: '||email||' Password: '||password);
exception
    when no_data_found then
        dbms_output.put_line('User not found.');
end;
/

```

## Insert and set default values

```
set serveroutput on
declare
    id user_table.user_id%type := '2007011';
    name user_table.name%type := 'Tashib';
    email user_table.email%type := 'tashib@gmail.com';
    password user_table.password%type := 'tashib';
begin
    insert into user_table(user_id, name, email, password) values (id, name, email, password);
    dbms_output.put_line('User inserted successfully.');
end;
/

```
## Row type
```
set serveroutput on
declare
    user user_table%rowtype;
begin
    select * into user from user_table where user_id = '2007009';
    dbms_output.put_line('User ID: '||user.user_id);
    dbms_output.put_line('Name: '||user.name);
    dbms_output.put_line('Email: '||user.email);
    dbms_output.put_line('Password: '||user.password);
end;
/

```
This will declare entire row at a time


## IF/ELSE and USER INPUT
```
SET SERVEROUTPUT ON;
DECLARE
    user_id_input VARCHAR2(20); 
    user user_table%ROWTYPE;
BEGIN
  
    user_id_input := '&Enter_your_user_id';

    SELECT * INTO user FROM user_table WHERE user_id = user_id_input;

  
    IF user.user_id IS NOT NULL THEN
      
        DBMS_OUTPUT.PUT_LINE('User ID: '||user.user_id);
        DBMS_OUTPUT.PUT_LINE('Name: '||user.name);
        DBMS_OUTPUT.PUT_LINE('Email: '||user.email);
        DBMS_OUTPUT.PUT_LINE('Password: '||user.password);
    ELSE
      
        DBMS_OUTPUT.PUT_LINE('User does not exist.');
    END IF;
END;
/

```

## LOOPS
```
SET SERVEROUTPUT ON;
DECLARE
   i number(2);
begin
   i:=1;
   loop
      dbms_output.put_line(i);
      i:=i+1;
      exit when i>20;
   end loop;
END;
/

```
This command will print values from 1 to 20

```
SET SERVEROUTPUT ON;
DECLARE
    user_row user_table%ROWTYPE; 
BEGIN
    
    FOR user_row IN (SELECT * FROM user_table) LOOP
    
        IF user_row.name = 'Raihan' THEN
            DBMS_OUTPUT.PUT_LINE('User ID: '||user_row.user_id);
            DBMS_OUTPUT.PUT_LINE('Name: '||user_row.name);
            DBMS_OUTPUT.PUT_LINE('Email: '||user_row.email);
            DBMS_OUTPUT.PUT_LINE('Password: '||user_row.password);
        END IF;
    END LOOP;
END;
/

```
# Cursors
//should be add

# procedures

```
CREATE OR REPLACE PROCEDURE SayHello(
    p_name IN VARCHAR2
)
IS
BEGIN
    DBMS_OUTPUT.PUT_LINE('Hello, ' || p_name || '!');
END;
/

```
Now call the procedure
```



BEGIN
    SayHello('Tamim');
END;
/

```



```
CREATE OR REPLACE PROCEDURE GetUserDetails(
    p_user_id IN VARCHAR2,
    p_user_name OUT VARCHAR2,
    p_user_email OUT VARCHAR2,
    p_user_password OUT VARCHAR2
)
IS
BEGIN
    SELECT name, email, password INTO p_user_name, p_user_email, p_user_password
    FROM user_table
    WHERE user_id = p_user_id;
END;
/

```
procedure created

```

DECLARE
    v_user_name user_table.name%TYPE;
    v_user_email user_table.email%TYPE;
    v_user_password user_table.password%TYPE;
BEGIN
    GetUserDetails('2007003', v_user_name, v_user_email, v_user_password); 
    DBMS_OUTPUT.PUT_LINE('User Name: ' || v_user_name);
    DBMS_OUTPUT.PUT_LINE('User Email: ' || v_user_email); 
    DBMS_OUTPUT.PUT_LINE('User Password: ' || v_user_password); 
END;
/
```
calling the procedure

# Function
```
CREATE OR REPLACE FUNCTION AddNumbers(
    p_num1 IN NUMBER,
    p_num2 IN NUMBER
)
RETURN NUMBER
IS
    v_sum NUMBER;
BEGIN
  
    v_sum := p_num1 + p_num2;
    RETURN v_sum;
END;
/

```

Now call the function

```
DECLARE
    result NUMBER;
BEGIN
    result := AddNumbers(10, 20);
    DBMS_OUTPUT.PUT_LINE('The sum is: ' || result);
END;
/

```
```
CREATE OR REPLACE FUNCTION GetUserEmail(
    p_user_id IN VARCHAR2
)
RETURN VARCHAR2
IS
    v_email VARCHAR2(100);
BEGIN
    
    SELECT email INTO v_email
    FROM user_table
    WHERE user_id = p_user_id;
    RETURN v_email;
    
END;
/
```

```
DECLARE
    result VARCHAR2(100); 
BEGIN
    result := GetUserEmail('2007003');
    DBMS_OUTPUT.PUT_LINE('The email is: ' || result);
END;
/

```


