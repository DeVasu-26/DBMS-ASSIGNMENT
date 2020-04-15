# deVasu-DBMS-Assignment
DBMS Assignment to Mr. Vipin sir

 NAME- VASUDEV
 ROLL No.- 20191238
 COURSE- B.Sc. STATISTICS (H)


Q.1)
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

(a)
Primary Key- Accession_Number in table LibraryBooks
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

(b)
mysql> set foreign_key_checks=Off;
       mysql> delete from librarybooks where accession_number=21826.46;
       mysql> delete from librarybooks where title="Database System Concepts";
       mysql> set foreign_key_checks=on;

(c)
mysql> update librarybooks set department="CS" where title="discrete maths";

(d)
mysql> select Title from librarybooks where department="CS";

(e)
mysql> select Title from librarybooks where department="CS" and author="navathe";

(f)
mysql> select Title from librarybooks l, issuedbooks i where l.accession_number=i.accession_number and l.department="CS";

(g)
mysql> select Title from librarybooks where price<500 and purchase_date between '1999/01/01' and '2004/01/01';
