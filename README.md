## Schedule-Management Database Project Demo



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


