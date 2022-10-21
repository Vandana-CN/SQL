use sql_training;
create table person(
	id int,
	firstname varchar(10),
    lastname varchar(10),
    age int
);
desc person;
create index idx_age on person(age);
alter table person drop index idx_age;

-- triggers

create table employeee (
id int,
name varchar(10),
dept varchar(10),
salary int,
address varchar(10),
city varchar(10)
);
insert into employeee values(5,'abc','it',2000,'mumbai','pune');
select * from employeee;
Delimiter $
create trigger properSalary
before insert on employeee for each row
Begin
if new.salary<0 then set new.salary=0;
end if;
end $
Delimiter ;
insert into employeee values(6,'xyz','hr',-1000,'tamilnadu','chennai');

Delimiter $
create trigger properCity
before update on employeee for each row
Begin
if new.city=" " then set new.city="trichy";
end if;
end $
Delimiter ;
update employeee set city=" " where city="chennai";

select * from employeee;


-- transactions

start transaction;
delete from employee where salary=0;
commit;
insert into employeee values(8,'def','hr',3000,'gujarat','ahmedabad');
rollback;

-- savepoint

start transaction;
select * from employeee;
update employeee set salary=salary+500;
savepoint pointone;
insert into employee values (9,'def','hr',3000,'gujarat','ahmedabad');
rollback to pointone;
commit;

-- after update trigger example
create table student(
	id int,
    name varchar(10),
    age int,
    city varchar(10)
);
insert into student values(1,"abc",22,"chennai"),(2,"def",21,"Mumbai"),(3,"ghi",23,"Pune");
select * from student;

create table studentchanges(age int);
Delimiter $
CREATE TRIGGER after_age_update
after update
on student for each row
begin
    if old.age>22 then
        insert into studentchanges(age)
        values(new.age);
end if;
end$$
Delimiter ;
update student set age=25 WHERE age=23;
SELECT * from student;
select * from studentchanges;
