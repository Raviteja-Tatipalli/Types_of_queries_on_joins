# Types_of_queries_on_joins
```sql
create database college;
use college;
```
```sqlcreate table student(
id int primary key,
name varchar(50),
age int not null,
marks int,
ranking int
);
```

```sqlcreate table student_record(
id int primary key,
course varchar(50),
joining_date int,
branch varchar(50)
);
```

```sql
insert into student
(id, name, age, marks, ranking)
values
(101, "tom", 24, 99, 1),
(102, "ian", 22, 95, 2),
(103, "nick", 21, 91, 5),
(104, "emily", 24, 94, 3),
(105, "emma", 22, 92, 4);
```

```sql
insert into student_record
(id, course, joining_date, branch)
values
(102, "btech", 2024, "ece"),
(104, "mtech", 2023, "ds"),
(105, "btech", 2024, "cse"),
(106, "med", 2022, "cb"),
(107, "btech", 2024, "ece");
```

select * from student;



```sql
select age, count(name) 
from student
group by age
order by age asc;
```

```sql
select *
from student
left join student_record
on student.id = student_record.id;
```

```sql
drop database college;
```

```sql
set sql_safe_updates = 0;
```

```sql
update student 
set age = "30"
where age = "21";
```

select * from student;

/*alter
add
drop
rename
modify 
change */

```sql
alter table student
add column grade varchar(1) default "a";
```

select * from student;

alter table student 
drop grade;

update student
set grade = "a"
where id = "101";

alter table student
change name fullname varchar(50);

delete from student
where marks < 92;

alter table student 
drop column age;

insert into student
(id, fullname, marks, ranking, grade)
values
(106, "jas", 98, 1, "a");

select avg(marks) from student;

select fullname, marks from student
where marks > (select avg(marks) from student);

select id from student
where id % 2 = 0;

select id, fullname from student
where id in (select id from student
where id % 2 != 0);

select * from student
where marks > 94;

select fullname from(select * from student
where marks > 95) as temp;

select course, avg(joining_date)
from student_record
group by course;

alter table student_record
change id student_id int;


create database college;
use college;

```sql
create table student(
id int primary key,
name varchar(50),
age int not null,
marks int,
ranking int
);
```

drop table student;

```sql
create table student_record(
id int primary key,
course varchar(50),
joining_date int,
branch varchar(50),
student_id int,
foreign key (student_id) references student(id)
on update cascade
on delete cascade
);
```

```sql
insert into student
(id, name, age, marks, ranking)
values
(101, "tom", 24, 99, 1),
(102, "ian", 22, 95, 2),
(103, "nick", 21, 91, 5),
(104, "emily", 24, 94, 3),
(105, "emma", 22, 92, 4);
```

```sql
insert into student_record
(id, course, joining_date, branch, student_id)
values
(102, "btech", 2024, "ece", 101),
(104, "mtech", 2023, "ds", 101),
(105, "btech", 2024, "cse", 102),
(106, "med", 2022, "cb", 104),
(107, "btech", 2024, "ece", 105);
```

```sql
update student
set id = 106
where id = 105;
```

```sql
select * from student;
select * from student_record;
```


drop database college;


create database record;
use record;

```sql
create table student(
id int primary key,
name varchar(50)
);
```

```sql
insert into student(id, name)
values(101, "tom"),
(102, "ian"),
(103, "robert"),
(104, "jas"),
(105, "david");
```

drop database record;

```sql
create table branch_details(
branch_id int,
branch_name varchar(50),
code int,
price int,
foreign key (branch_id) references student(id)
on update cascade
on delete cascade
);
```

```sql
insert into branch_details(branch_id, branch_name, code, price)
values(101, "data", 111, 10),
(102, "network", 222, 20),
(103, "manage", 333, 30),
(104, "business", 444, 40),
(105, "data science", 555, 50);
```

```sql
update student
set id = 111
where id = 105;
```

```sql
delete from student
where id = 101;
```

```sql
select * from branch_details;
```


-- Choco shipments


```sql
create view bd as
select branch_name, code, price from branch_details;
```
 
```sql
create database ac_chocos;
use ac_chocos;
```

```sql
select * from shipments;
select * from products;
```

```sql
select product, s.date, amount, boxes from shipments s;
```

```sql
select * from shipments s
where s. `sales person` = "sp02" and s.geo = "g3"
order by s.amount desc;
```

```sql
select * from shipments_new s 
where s.date between "2023-1-1" and "2023-1-31";
```
```sql
select * from shipments_new s
where extract(year_month from s.date) = 202301;
```

```sql
select * from shipments_new s 
where s.`sales person` = "sp02" 
or s.`sales person` = "sp03" 
or s.`sales person` = "sp12";
```

```sql
select * from shipments_new s 
where s.`sales person` in ("sp02","sp03","sp12","sp15");
```

```sql
select * from products
where product like "%choco%";
```

```sql
select * from people
where `sales person` like "s%" and location = "hyderabad";
```

```sql
select date, amount, boxes, round(amount/boxes, 1) as "amount per box" from shipments_new
where extract(year_month from date) = 202302;
```

```sql
select * from people
where `sales person` like "subba%";
```

```sql
select * from shipments_new
where `sales person` = "sp11";
```

```sql
select p.`sales person`, s.date, s.boxes, s.amount from shipments_new s
join people p on p.`sp id` = s. `Sales Person`
where p.`sales person` like "subba%";
```

```sql
select extract(year_month from s.date) as grouped_by_month, sum(s.boxes)
from shipments_new s
join people p on p.`sp id` = s. `Sales Person`
where p.`sales person` like "\subba%"
group by extract(year_month from s.date);
```

```sql
select p.`sales person`, g.geo, s.date, s.amount
from shipments_new s
join people p on p.`sp id` = s. `Sales Person`
join geo g on g.Geoid = s.geo 
where 
p.`sales person` like "subba%" and g.geo = "usa";
```

```sql
select extract(year_month from s.date) AS MONTHLY, min(s.amount) , max(s.amount)
from shipments_new s
group by extract(year_month from s.date)
order by min(s.amount) asc, max(s.amount) desc;
```

```sql
select s.`sales person`, count(*) as `total count of shipments`, sum(amount), sum(boxes)
from shipments_new s
join geo g on g.GeoID = s.geo
where extract(year_month from s.date) = 202303
group by s.`sales person`
order by `sales person`;
```



```sql
select * from geo;
drop database ac_chocos;
```

-- The end
