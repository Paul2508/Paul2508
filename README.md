- 👋 Hi, I’m @Paul2508
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
Paul2508/Paul2508 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->

create database emp; --creating a new schema

create table emp.department 
( 
id INT NOT NULL AUTO_INCREMENT,
name VARCHAR(30) NOT NULL,
PRIMARY KEY (id),
);


create table emp.role
(
id INT NOT NULL,
title VARCHAR(30),
salary DECIMAL,
department_id INT,
PRIMARY KEY (id),
FOREIGN KEY (department_id) REFERENCES emp.department(id)
);

create table emp.employee
(
id INT NOT NULL AUTO_INCREMENT,
first_name VARCHAR(30),
last_name VARCHAR(30),
role_id INT,
manager_id INT, 
PRIMARY KEY (id),
FOREIGN KEY (role_id) REFERENCES emp.role(id)
);

Creating Admin user:

create user 'admin'@'localhost' identified by 'password';

Providing privileges to admin to perform the changes.
 
grant select, insert, update, delete on emp.* to 'admin'@'localhost';

Creating Manager user.

create user 'manager'@'localhost' identified by 'password';

Providing privileges for limited access (view and update).

grant select emp.employee to 'manager'@'localhost';

create user 'department'@'localhost' identified by 'password';

grant select on emp.employee to 'department'@'localhost';

select d.name as department, sum(r.salary) as Total
from emp.department d inner join emp.role r 
on d.id = r.department_id
group by department;

