# DBMS-Assignment
DBMS Assignment to Mr. Vipin sir

 NAME- VASUDEV
 ROLL No.- 20191238
 COURSE- B.Sc. STATISTICS (H)


Q.3)
mysql> create database twowheeler;

mysql> create table customer(
    -> CustId varchar(20) primary key,
    -> email varchar(50) not null,
    -> Name char(30) not null,
    -> phone varchar(10) unique,
    -> ReferrerID varchar(20));

mysql> create table BicycleModel(
    -> ModelNo varchar(10) primary key,
    -> Manufacturer Char(20) not null,
    -> Style Varchar(20) not null);

mysql> create table Bicycle(
    -> BicycleId varchar(20) primary key,
    -> DatePurchased date not null,
    -> Color Char(10) not null,
    -> CustId varchar(20) not null,
    -> ModelNo varchar(10) not null,
    -> foreign key(CustId) references customer(CustId),
    -> foreign key(ModelNo) references BicycleModel(ModelNo));

mysql> create table Service(
    -> StartDate date not null,
    -> BicycleId varchar(20) not null,
    -> EndDate date not null,
    -> Foreign key(BicycleId) references Bicycle(BicycleId));


(a)
Primary Key - CustId in table Customer
                             ModelNo in table BicycleModel
                             BicycleId in table Bicycle
         Foreign Key- CustId in table Bicycle
                             ModelNo in table Bicycle
                             BicycleId in table Service

mysql> insert into customer values(1001,"param1245@gmail.com","Param Singh",9873645321,"C1");
mysql> insert into customer values(1002,"ankit4373@gmail.com","Ankit Kumar",8373876327,"A2");
mysql> insert into customer values(1003,"rajatkumar8653@gmail.com","Rajat Kumar",9375472814,"C3");
mysql> insert into customer values(1004,"sumanjoshi7368@gmail.com","Suman Joshi",8293765392,"B7");
mysql> insert into customer values(1005,"rashmitiwari3753@gmail.com","Rashmi Tiwari",9375428765,"C5");

mysql> insert into bicyclemodel values("M101","Honda","Cruiser");
mysql> insert into bicyclemodel values("M102","Hero","Scooty");
mysql> insert into bicyclemodel values("M103","Apache","Dirt bike");
mysql> insert into bicyclemodel values("M104","Hero","Bike");
mysql> insert into bicyclemodel values("M105","Hero","Sport");

mysql> insert into bicycle values("B501",'2019-02-05',"Red","1002","M101");
mysql> insert into bicycle values("B502",'2018-05-22',"Silver","1001","M105");
mysql> insert into bicycle values("B503",'2020-01-03',"Red","1004","M104");
mysql> insert into bicycle values("B504",'2019-04-17',"blue","1003","M103");
mysql> insert into bicycle values("B505",'2020-02-08',"black","1002","M102");

mysql> insert into service values('2019-09-09','B505',"2019-09-12");
mysql> insert into service values('2018-10-10','B502','2018-10-12');
mysql> insert into service values('2018-04-24','B502','2019-04-26');
mysql> insert into service values('2019-05-17','B501','2019-05-19');
mysql> insert into service values('2020-01-18','B502','2020-01-20');

(b)
mysql> Select * from customer where custID in(Select custid from bicycle where modelno in(select Modelno from bicyclemodel where manufacturer="Honda"));

(c)
mysql> Select * from bicyclemodel where modelno in(select modelno from bicycle where custid in(select custid from customer where referrerId="C1"));

(d)
mysql> select bm.manufacturer from bicycle as bi, bicyclemodel as bm where bi.modelno=bm.modelno  and bi.color="red";

(e)
mysql> select modelno from bicycle where bicycleid in(select distinct bicycleid from service);

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


