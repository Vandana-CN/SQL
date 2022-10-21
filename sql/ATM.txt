use sql_training;
create table atm(
accno int,
balalnce int);
insert into atm values(10,10000);
start transaction;
select * from account;
update atm set balalnce=balalnce+500 where accno=10;
savepoint mysavepoint;
update atm set balalnce=balalnce-1000 where accno=10;
rollback to mysavepoint;
commit;