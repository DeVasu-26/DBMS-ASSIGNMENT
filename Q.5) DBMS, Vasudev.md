# DBMS-Assignment
DBMS Assignment to Mr. Vipin sir

 NAME- VASUDEV
 ROLL No.- 20191238
 COURSE- B.Sc. STATISTICS (H)


Q.5)
mysql> create database product;
mysql> use product;

mysql> create table suppliers(
    -> Sno int(8) primary key,
    -> Sname varchar(20) not null,
    -> Status char(20) not null,
    -> Scity char(30) not null);

mysql> create table Parts(
    -> PNo int(8) primary key,
    -> Pname varchar(20) not null,
    -> Colour varchar(20) not null,
    -> Weight int(4) not null,
    -> City char(20) not null);

mysql> create table Project(
    -> Jno int(8) Primary key,
    -> Jname char(20) not null,
    -> Jcity char(20) not null);

mysql> create table  Shipment(
    -> Sno varchar(20) not null,
    -> Pno int(8) not null,
    -> Jno int(8) not null,
    -> Quantity int(8) not null,
    -> foreign key(Sno) references suppliers(Sno),
    -> foreign key(Pno) references Parts(Pno),
    -> Foreign key(Jno) references Project(Jno));

mysql> insert into suppliers values("101","S1",30,"London");
mysql> insert into suppliers values("102","S2",19,"New York");
mysql> insert into suppliers values("103","S1",22,"Paris");
mysql> insert into suppliers values("104","S2",70,"Los Angeles");
mysql> insert into suppliers values("104","S2",70,"Los Angeles");

mysql> insert into parts values( "501","P1","Black",16,"Paris");
mysql> insert into parts values( "502","P2","Red",40,"London");
mysql> insert into parts values( "503","P3","Gray",20,"London");
mysql> insert into parts values( "503","P2","Green",60,"Singapore");
mysql> insert into parts values( "505","P2","Black",10,"New York");

mysql> insert into project values(1001,"J1","London");
mysql> insert into project values(1002,"J2","New York");
mysql> insert into project values(1003,"J3","New York");
mysql> insert into project values(1004,"J4","Singapore");
mysql> insert into project values(1005,"J4","Delhi");

mysql> insert into shipment values(101,504,1002,250);
mysql> insert into shipment values(103,505,1003,100);
mysql> insert into shipment values(105,502,1003,500);
mysql> insert into shipment values(101,503,1001,300);
mysql> insert into shipment values(102,501,1005,750);
mysql> insert into shipment values(101,501,1002,100);

(a)
Primary Key- Sno in table Suppliers
                            Pno in table Parts
                            Jno in table Project

        Foreign Key- Sno in table Shipment
                            Pno in table Shipment
                            Jno in table Shipment

(b)
mysql> select Sno from suppliers where scity="Paris" and Status>20;

(c)
mysql> Select * from suppliers where Sno in(select Sno from shipment where Pno in(select Pno from parts where Pname="P2")) Order by sno;

(d)
mysql> Select Sname from suppliers where Sno in(Select distinct sno from shipment where Pno in(select Pno from parts where Pname!="P2"));

(e)
mysql> select s.Sno, s.Pno, s.Jno, s.Quantity, s.quantity*p.weight as "Total_shipment_weight" from shipment as s, parts as p where s.pno=p.pno;

(f)
mysql> Select * from shipment where quantity between 300 and 750;

(g)
mysql> select Pno from parts where weight>16 or pno in(select pno from shipment where sno in(select s.sno from shipment as s, suppliers as su where s.sno=su.sno and su.sname="S2"));

(h)
mysql> select city from parts where colour="Red" and Pno in(select pno from shipment where quantity>5);

(i)
mysql> select * from parts where pno in(select Pno from shipment where sno in(select sno from suppliers where Scity="London"));

(j)
mysql> select Pno from shipment where sno in(select sno from suppliers where scity="London") and Jno in(Select jno from project where Jcity="London");

(k)
mysql> select count(distinct(Jno)) as "No. of Project Supplied by supplier S1" from shipment where sno in(select sno from suppliers where Sname="S1");

(l)
mysql> select count(*) from parts where Pno in(Select Pno from shipment where sno in(select Sno from suppliers where sname ="S1")) and Pname="P1";
