# IMPLEMENTATION-OF-IMPLICIT-AND-EXPLICIT-CURSOR-TO-MANIPULATE-A-TABLE-IN-PL-SQL

AIM:

To manipulate a table using Implicit and Explicit Cursors.

PROCEDURE:

PL/SQL - Cursors

A cursor is a pointer to this context area. PL/SQL controls the context area through a cursor. A cursor holds the rows (one or more) returned by a SQL statement. The set of rows the cursor holds is referred to as the active set.

There are two types of cursors.

• Implicit cursors

• Explicit cursors

Implicit Cursors

Implicit cursors are automatically created by Oracle whenever an SQL statement is executed, when there is no explicit cursor for the statement. Programmers cannot control the implicit cursors and the information in it. Whenever a DML statement (INSERT, UPDATE and DELETE) is issued, an implicit cursor is associated with this statement. For INSERT operations, the cursor holds the data that needs to be inserted. For UPDATE and DELETE operations, the cursor identifies the rows that would be affected. In PL/SQL, you can refer to the most recent implicit cursor as the SQL cursor, which always has attributes such as %FOUND, %ISOPEN, %NOTFOUND, and %ROWCOUNT. The SQL cursor has additional attributes, %BULK_ROWCOUNT and %BULK_EXCEPTIONS, designed for use with the FORALL statement. The following table provides the description of the most used

attributes −
S.No Attribute & Description

1 %FOUND
Returns TRUE if an INSERT, UPDATE, or DELETE statement affected one or more rows or a SELECT INTO statement returned one or more rows. Otherwise, it returns FALSE.

2 %NOTFOUND
The logical opposite of %FOUND. It returns TRUE if an INSERT, UPDATE, or DELETE statement affected no rows, or a SELECT INTO statement returned no rows. Otherwise, it returns false

3 %ISOPEN
Always returns FALSE for implicit cursors, because Oracle closes the SQL cursor automatically after executing its associated SQL statement.

4 %ROWCOUNT
Returns the number of rows affected by an INSERT, UPDATE, or DELETE statement, or returned by a SELECT INTO statement.

Any SQL cursor attribute will be accessed as sql%attribute_name as shown below in the

example.

Explicit Cursors

Explicit cursors are programmer-defined cursors for gaining more control over the context area. An explicit cursor should be defined in the declaration section of the PL/SQL Block. It is created on a SELECT Statement which returns more than one row.

The syntax for creating an explicit cursor is −

CURSOR cursor_name IS select_statement;

Working with an explicit cursor includes the following steps −

• Declaring the cursor for initializing the memory

• Opening the cursor for allocating the memory

• Fetching the cursor for retrieving the data

• Closing the cursor to release the allocated memory

Declaring the Cursor

Declaring the cursor defines the cursor with a name and the associated SELECT statement.

For example −

CURSOR c_customers IS SELECT id, name, address FROM customers;

Opening the Cursor

Opening the cursor allocates the memory for the cursor and makes it ready for fetching the rows returned by the SQL statement into it. For example, we will open the above defined cursor as follows −

OPEN c_customers;

Fetching the Cursor

Fetching the cursor involves accessing one row at a time. For example, we will fetch rows from the above-opened cursor as follows −

FETCH c_customers INTO c_id, c_name, c_addr;

Closing the Cursor

Closing the cursor means releasing the allocated memory. For example, we will close the
above-opened cursor as follows −

CLOSE c_customers;

PROGRAM :

1.Program to update the table and increase the salary of each customer by 500 Using implicit Cursor

SQL>Select * from customers;
+----+----------+-----+-----------+----------+
| ID | NAME | AGE | ADDRESS | SALARY |
+----+----------+-----+-----------+----------+
| 1 | Ramesh | 32 | Ahmedabad | 2000.00 |
| 2 | Khilan | 25 | Delhi | 1500.00 |
| 3 | kaushik | 23 | Kota | 2000.00 |
| 4 | Chaitali | 25 | Mumbai | 6500.00 |
| 5 | Hardik | 27 | Bhopal | 8500.00 |
| 6 | Komal | 22 | MP | 4500.00 |
+----+----------+-----+-----------+----------+

SQL>DECLARE

2 total_rows number(2);

3 BEGIN

4 UPDATE customers

5 SET salary = salary + 500;

6 IF sql%notfound THEN

7 dbms_output.put_line('no customers selected');

8 ELSIF sql%found THEN

9 total_rows := sql%rowcount;

10 dbms_output.put_line( total_rows || ' customers selected ');

11 END IF;

12 END;

Output:

6 customers selected

PL/SQL procedure successfully completed.

SQL>Select * from customers;

+----+----------+-----+-----------+----------+
| ID | NAME | AGE | ADDRESS | SALARY |
+----+----------+-----+-----------+----------+
| 1 | Ramesh | 32 | Ahmedabad | 2500.00 |
| 2 | Khilan | 25 | Delhi | 2000.00 |
| 3 | kaushik | 23 | Kota | 2500.00 |
| 4 | Chaitali | 25 | Mumbai | 7000.00 |

| 5 | Hardik | 27 | Bhopal | 9000.00 |
| 6 | Komal | 22 | MP | 5000.00 |
+----+----------+-----+-----------+----------+

2. Program to illustrate the concepts of explicit cursors &minua;

SQL>DECLARE

2 c_id customers.id%type;

3 c_name customers.name%type;

4 c_addr customers.address%type;

5 CURSOR c_customers is

6 SELECT id, name, address FROM customers;

7 BEGIN

8 OPEN c_customers;

9 LOOP

10 FETCH c_customers into c_id, c_name, c_addr;

11 EXIT WHEN c_customers%notfound;

12cdbms_output.put_line(c_id || ' ' || c_name || ' ' || c_addr);

13 END LOOP;

14 CLOSE c_customers;

15 END;

/

Output:

1 Ramesh Ahmedabad

2 Khilan Delhi

3 kaushik Kota

4 Chaitali Mumbai

5 Hardik Bhopal

6 Komal MP

PL/SQL procedure successfully completed.

RESULT:

Thus the manipulation of a table using Implicit and Explicit Cursors has been verified and executed successfully.
