create table hospital(Pno int,name varchar(20),Age int,Department varchar(100),Dateofadm date,charges int,sex char(1),primary key(Pno));
insert into hospital values
(1,"Arpita",62,"Surgery","1998-01-12",300,"M"),
(2,"Zarina",22,"ENT","1998-12-12",250,"F"),
(3,"Kareem",32,"Orthopedic","1998-02-19",200,"M"),
(4,"Arun",12,"Surgery","1998-01-11",300,"M"),
(5,"Zubin",30,"ENT","1998-01-12",250,"M"),
(6,"Ketaki",16,"ENT","1998-02-24",250,"F"),
(7,"Ankita",29,"Cardiology","1998-02-20",800,"F"),
(8,"Zareen",45,"Gynaecologist","1998-02-22",300,"F"),
(9,"Kush",19,"Cardiology","1998-01-13",800,"M"),
(10,"Shilpa",23,"Nuclear Medicine","1998-01-20",400,"F");

start transaction;
desc hospital;
commit;

start transaction;
select concat(name,' age of ',age,' admitted on ',dateofadm) as details from hospital;
commit;

start transaction;
alter table hospital add Address char(20);
commit;

start transaction;
alter table hospital change Address Address char(25);
commit;

start transaction;
alter table hospital change Address Address varchar(25);
commit;

start transaction;
alter table hospital rename column Address to Home_Address;
commit;

start transaction;
Alter table Hospital drop column Home_Address ;
commit;

start transaction;
alter table hospital RENAME TO hospital_Data;
commit;

start transaction;
update hospital_data set Age=30 where Pno=7 ;
commit;

select * from hospital_data;

start transaction;
truncate hospital_data ;
commit;

start transaction;
drop table hospital_data ;
commit;



create table agechanges(age int);
Delimiter $
CREATE TRIGGER patient_age_update
after update
on hospital_data for each row
begin
    if old.Pno=7 then
        insert into agechanges(age) 
        values(new.age);
end if;
end$$
Delimiter ;
update hospital_data set age=30 where Pno=7;
SELECT * from hospital_data;
select * from agechanges;

select * from hospital_data;	


