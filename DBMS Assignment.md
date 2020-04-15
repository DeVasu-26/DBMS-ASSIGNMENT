# deVasu-DBMS-Assignment
DBMS Assignment to Mr. Vipin sir


1.
mysql> create database du_library;

mysql> create table LibraryBooks(
    -> Accession_Number decimal(10,5) primary key,
    -> Title varchar(30) not null,
    -> Author varchar(50) not null,
    -> Department varchar(50) not null,
    -> Purchase_Date date not null,
    -> Price decimal(7,2) not null);

mysql> Create table IssuedBooks(
    -> Accession_Number decimal(10,5) not null,
    -> Borrower Varchar(30) not null
    -> foreign key (Accession_Number) references LibraryBooks(Accession_Number));

Q (a)Primary Key- Accession_Number in table LibraryBooks
        Foreign Key- Accession_Number in table IssuedBooks
mysql> insert into LibraryBooks values(51235.56,"Introduction to Matrices","S.C. Gupta","Statistics",'1997-01-12',105.00);
mysql> insert into LibraryBooks values(21826.46,"Database System Concepts","Bharat Kumar Singh","CS",'2001/05/30',620.00);
mysql>  insert into LibraryBooks values(121.4345,"Fundamental of Statistics","V.K. Kapoor","Statistics",'2005/03/31',550.00);
mysql> insert into LibraryBooks values(76389.4647,"Programing in R","Navathe","CS",'2002/07/21',499.00);
mysql> insert into LibraryBooks values(6737.84,"Discrete Maths","R. Kapoor","Mathematics",'1999/09/04',450.00);

mysql> insert into IssuedBooks values( 21826.46,"Raman Singh");
mysql> insert into IssuedBooks values( 121.4345,"Sumit Kandpal");
mysql> insert into IssuedBooks values( 6737.84,"Rahul Tatrari");
mysql> insert into IssuedBooks values( 21826.46,"Shruti Bist");
mysql> insert into IssuedBooks values( 76389.4647,"Rohit Tiwari");

Q(b) mysql> set foreign_key_checks=Off;
       mysql> delete from librarybooks where accession_number=21826.46;
       mysql> delete from librarybooks where title="Database System Concepts";
       mysql> set foreign_key_checks=on;

Q(c) mysql> update librarybooks set department="CS" where title="discrete maths";

Q(d) mysql> select Title from librarybooks where department="CS";

Q(e) mysql> select Title from librarybooks where department="CS" and author="navathe";

Q(f) mysql> select Title from librarybooks l, issuedbooks i where l.accession_number=i.accession_number and l.department="CS";

Q(g) mysql> select Title from librarybooks where price<500 and purchase_date between '1999/01/01' and '2004/01/01';



------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

2.
mysql> create database cs_student;

mysql> create table personal_informartion(
    -> Roll_no int(10) primary key,
    -> Name char(30) not null,
    -> DOB date not null,
    -> Address varchar(70) not null,
    -> Marks_in_12th int(2) not null,
    -> Phone_number Varchar(10) not null);

mysql> create table Paper_Details(
    -> Paper_Code int(4) primary key,
    -> NameofPaper char(30) unique);

mysql> create table Academic_Details(
    -> Roll_no int(10) primary key,
    -> Paper_code int(4) not null,
    -> Attendence int(3) not null,
    -> Marks int(3) not null,
    -> foreign key(roll_no) references personal_informartion(roll_no),
    -> foreign key(paper_code) references Paper_details(paper_code));

Q (a) Primary key - Roll_no in table personal_informartion
                             Paper_code in table Paper_details
        Foreign key - Roll_no in table Academic_Details
                            Paper_code in table Academic_Details 

mysql> insert into personal_informartion values(1201,"Amit Kandpal",'2001-01-04',"Delhi",91,9102829875);
mysql> insert into personal_informartion values(1205,"Anuj Joshi",'2001-04-29',"Uttarakhand",89,9748483743);
mysql> insert into personal_informartion values(1209,"Bhawana Arora",'2000-03-19',"Delhi",94,9837643368);
mysql> insert into personal_informartion values(1214,"Ishita Pandey",'2001-09-21',"Uttar Pradesh",97,9637453672);
mysql> insert into personal_informartion values(1219,"Pooja Singh",'2001-11-09',"Delhi",92,9764563726);

mysql> insert into paper_details value(1,"Descriptive Statistics");
mysql> insert into paper_details value(2,"English Communication");
mysql> insert into paper_details value(3,"Algebra");
mysql> insert into paper_details value(4,"Introduction to Matrices");
mysql> insert into paper_details value(5,"Database management system");

mysql> insert into Academic_details values(1201,2,80,70);
mysql> insert into Academic_details values(1205,2,70,90);
mysql> insert into Academic_details values(1214,2,65,91);
mysql> insert into Academic_details values(1214,2,65,91);
mysql> insert into Academic_details values(1219,1,75,65);

Q(b) mysql> select pd.paper_code, pd.nameofpaper, pi.name from paper_details as pd, personal_informartion as pi where paper_code=2 and pi.roll_no in(select roll_no from academic_details where paper_code=2 and attendence>75 and marks>60);

Q (c) mysql> select name from personal_informartion as pi, academic_details as ad where pi.roll_no=ad.roll_no and ad.marks>60 and ad.paper_code=1;

Q (d) mysql> select pi.name, ad.attendence, ad.marks from personal_informartion as pi, academic_details as ad where pi.roll_no=ad.roll_no;

Q (e) mysql> select name from personal_informartion as pi, academic_details as ad where pi.roll_no=ad.roll_no and pi.roll_no=(select roll_no from academic_details where marks=(select max(marks) from academic_details));


-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

3.
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


Q (a) Primary Key - CustId in table Customer
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

Q (b) mysql> Select * from customer where custID in(Select custid from bicycle where modelno in(select Modelno from bicyclemodel where manufacturer="Honda"));

Q(c) mysql> Select * from bicyclemodel where modelno in(select modelno from bicycle where custid in(select custid from customer where referrerId="C1"));

Q(d) mysql> select bm.manufacturer from bicycle as bi, bicyclemodel as bm where bi.modelno=bm.modelno  and bi.color="red";

Q(e) mysql> select modelno from bicycle where bicycleid in(select distinct bicycleid from service);

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

4. mysql> create database employee_details;
    mysql> use employee_details;
  
   mysql> create table employee(
    -> Person_name char(30) primary key,
    -> Street char(30) not null,
    -> city char(15) not null);

   mysql> create table Company(
    -> Company_name varchar(30) Primary key,
    -> City char(15));

   mysql> create table Works(
    -> Person_name  char(30),
    -> Company_name varchar(30),
    -> Salary decimal(10,2),
    -> foreign key(Person_name) references employee(Person_name),
    -> foreign key(Company_name) references Company(Company_name));

   mysql> Create table manages(
    -> Person_name char(30),
    -> Manager_name char(30),
    -> foreign key(Person_name) references employee(Person_name));

mysql> insert into employee values("Rashmi","23/34 B block","Delhi");
mysql> insert into employee values("Teena","454/4 V block","Gurgaon");
mysql> insert into employee values("Ananya","65/6 A block","Gurgaon");
mysql> insert into employee values("Kritika","87/2 D block","Lucknow");
mysql> insert into employee values("Gaurav","74/2 F block","Gaziabad");
mysql> insert into employee values("Saurav","54/2 G block","Noida");
mysql> insert into employee values("Kashish","347-5 A block","Noida");
mysql> insert into employee values("Pawan","65/8 V block","Gurgaon");
mysql> insert into employee values("Nikhil","62/7 d block","Sitapur");
mysql> insert into employee values("Neha","91/8 C block","Gaziabad");

mysql> insert into company values("Samba Bank","Delhi");
mysql> insert into company values("NCB Bank","Gurgaon");
mysql> insert into company values("Axis Bank","Noida");
mysql> insert into company values("SBI bank","Lucknow");
mysql> insert into company values("Kotak Bank","Gaziabad");

mysql> insert into works values("Rashmi","Samba Bank", 20000);
mysql> insert into works values("Teena","NCB Bank",15000);
mysql> insert into works values("Ananya","Samba Bank",5000);
mysql> insert into works values("Kritika","SBI Bank",8000);
mysql> insert into works values("Gaurav","Axis Bank",10000);
mysql> insert into works values("Saurav","NCB Bank",20000);
mysql> insert into works values("Kashish","Kotak Bank",15000);
mysql> insert into works values("Pawan","Axis Bank",20000);
mysql> insert into works values("Nikhil","SBI Bank",12000);
mysql> insert into works values("Neha","Kotak Bank",18000);


Q (a) Primary Key- Person_name in table employee
                            Company_name in table company
        Foreign Key- Person_name in table works
                            Company_name in table works
                            Person_name in table manages

Q (b) mysql> alter table employee add column email varchar(20);

Q (c) mysql> select distinct(manager_name) from manages as m, works as w where m.person_name=w.person_name and (w.company_name="Samba bank" or w.Company_name="NCB Bank");

Q (d) mysql> select e.Person_name, e.Street, e.City, w.salary from employee as e, works as w where e.person_name=w.person_name and w.company_name="Samba Bank" and w.salary>10000;

Q (e) mysql> select e.person_name from employee as e, works as w, company as c where e.person_name=w.person_name and e.city=c.city and w.company_name=c.company_name;

Q (f) mysql> select company_name, max(salary), min(salary), avg(salary) from works group by company_name;

Q (g) mysql> select company_name, sum(salary), count(company_name) as "number of employees" from works group by company_name;

Q (h) mysql> select company_name,max(salary) from works;
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
5.

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

Q (a) Primary Key- Sno in table Suppliers
                            Pno in table Parts
                            Jno in table Project

        Foreign Key- Sno in table Shipment
                            Pno in table Shipment
                            Jno in table Shipment

Q (b) mysql> select Sno from suppliers where scity="Paris" and Status>20;

Q (c) mysql> Select * from suppliers where Sno in(select Sno from shipment where Pno in(select Pno from parts where Pname="P2")) Order by sno;

Q (d) mysql> Select Sname from suppliers where Sno in(Select distinct sno from shipment where Pno in(select Pno from parts where Pname!="P2"));

Q (e) mysql> select s.Sno, s.Pno, s.Jno, s.Quantity, s.quantity*p.weight as "Total_shipment_weight" from shipment as s, parts as p where s.pno=p.pno;

Q (f) mysql> Select * from shipment where quantity between 300 and 750;

Q (g) mysql> select Pno from parts where weight>16 or pno in(select pno from shipment where sno in(select s.sno from shipment as s, suppliers as su where s.sno=su.sno and su.sname="S2"));

Q (h) mysql> select city from parts where colour="Red" and Pno in(select pno from shipment where quantity>5);

Q (i) mysql> select * from parts where pno in(select Pno from shipment where sno in(select sno from suppliers where Scity="London"));

Q (j) mysql> select Pno from shipment where sno in(select sno from suppliers where scity="London") and Jno in(Select jno from project where Jcity="London");

Q (k) mysql> select count(distinct(Jno)) as "No. of Project Supplied by supplier S1" from shipment where sno in(select sno from suppliers where Sname="S1");

Q (l) mysql> select count(*) from parts where Pno in(Select Pno from shipment where sno in(select Sno from suppliers where sname ="S1")) and Pname="P1";

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

