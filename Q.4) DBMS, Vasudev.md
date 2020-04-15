# DBMS-Assignment
DBMS Assignment to Mr. Vipin sir

 NAME- VASUDEV
 ROLL No.- 20191238
 COURSE- B.Sc. STATISTICS (H)


Q.4)
mysql> create database employee_details;
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


(a)
Primary Key- Person_name in table employee
                            Company_name in table company
        Foreign Key- Person_name in table works
                            Company_name in table works
                            Person_name in table manages

(b)
mysql> alter table employee add column email varchar(20);

(c)
mysql> select distinct(manager_name) from manages as m, works as w where m.person_name=w.person_name and (w.company_name="Samba bank" or w.Company_name="NCB Bank");

(d)
mysql> select e.Person_name, e.Street, e.City, w.salary from employee as e, works as w where e.person_name=w.person_name and w.company_name="Samba Bank" and w.salary>10000;

(e)
mysql> select e.person_name from employee as e, works as w, company as c where e.person_name=w.person_name and e.city=c.city and w.company_name=c.company_name;

(f)
mysql> select company_name, max(salary), min(salary), avg(salary) from works group by company_name;

(g)
mysql> select company_name, sum(salary), count(company_name) as "number of employees" from works group by company_name;

(h)
mysql> select company_name,max(salary) from works;





