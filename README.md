# Security Analysis with SQL

## Objective


In a simulated environment, I was tasked with identifying potential security breaches at a hypothetical company using SQL. This involved analyzing failed login attempts after business hours, examining login activity on specific dates, and filtering login attempts from outside certain geographical locations. Additionally, I retrieved data on employees in specific departments for security updates and used SQL joins to link employee and machine data. These tasks enhanced my understanding of SQL in a security context.


### Skills Learned

- Advanced proficiency in crafting and optimizing SQL queries for data retrieval and analysis
- Ability to use SQL filters, logical operators, and SQL joins to identify potential security breaches and correlate data across multiple tables
- Enhanced problem-solving skills through practical application of SQL in a simulated security environment.



## Procedure

### Retrieving Failed Login Attempts Made After Hours

My first task was to investigate a potential security breach that occurred after business hours (18:00). To find a good starting point, I needed to obtain a list of all failed login attempts made after 18:00. This information could be found in the table log_in_attempts. The following code demonstrates the SQL query I used to retrieve this information. Its output is also displayed.

![image](https://github.com/user-attachments/assets/1f352b69-ed7c-4eed-b0cf-11a026db6a8f)

I started the query with SELECT * FROM log_in_attempts, which selects all data from the log_in_attempts table. The first condition, where login_time > '18:00', filters for the login attempts after 18:00. The second condition,  success = FALSE, filters for unsuccessful login attempts. Nineteen total attempts were found. 

<br></br>

### Retrieving Login Attempts From Specific Dates

Potentially suspicious activity was noticed on 2022-05-09.  To investigate further, I needed to gather all failed login attempts on this date and the day before. The following code demonstrates how I created a SQL query to filter for login attempts between 2022-05-08 and 2022-05-09. 

![image](https://github.com/user-attachments/assets/65d03840-a23c-44e4-9256-3e9306981675)

I started the query by selecting all data from the log_in_attempts table by typing SELECT * FROM log_in_attempts. The first condition, WHERE login_date = '2022-05-09', filtered for logins on 2022-05-09. Using an OR operator, I added a second condition, login_date = '2022-05-08', to filter for login attempts made on 2022-05-08. Please note that this image shows only a portion of the results. A total of 75 login attempts were found.

<br></br>

### Retrieving Login Attempts Outside of Mexico

Another scan detected unusual activity concerning login attempts. However, the team determined that this suspicious activity must have originated from a location outside of Mexico. For this task, I used the following query (highlighted in gray)  to return all login attempts in countries other than Mexico.

![image](https://github.com/user-attachments/assets/6bb799e8-d35c-4f2d-b6b1-7bf777e2ef78)

I started by selecting all data from the log_in_attempts table. Since our investigation aimed to find all login attempts that were NOT from Mexico,  I used a WHERE clause with NOT to filter for countries other than that specific point of origin. Another critical thing to note is that the country column accepts both country names and abbreviations ( ‘MEXICO’ and ‘MEX’ are both valid). I used the LIKE operator with the pattern 'MEX%' to accommodate for this. The percentage sign (%) serves as a wildcard for matching any sequence of characters following ‘MEX.’ A total of 144 attempts from outside of Mexico were found.

<br></br>

### Retrieving Employees in Marketing

The security team wanted to update the employee machines in the Marketing department as part of their hardening process. More specifically, the machines in all ‘East’ offices needed to be updated.

![image](https://github.com/user-attachments/assets/bd678e8c-37bb-4548-bdbf-780c04e671e7)

I began by retrieving all records from the employees table. I applied a WHERE clause using the AND operator to narrow down the results to specific criteria. This clause filters for employees in the Marketing department and located in the East building. The condition department = 'Marketing' isolates employees within the Marketing department. Additionally, I used the LIKE operator with the pattern 'East%' in the office column to match employees whose office numbers start with 'East', indicating their location in the East building. Seven employees were found.

<br></br>

### Retrieving Employees in Sales or Finance

The employee machines in the Finance and Sales departments also needed to receive their own separate updates. The following code demonstrates how I used a query to filter for machines from employees in either the Sales or Finance departments.

![image](https://github.com/user-attachments/assets/bf11d66b-8274-48ad-824e-e71c952073ea)

I selected all data from the employees table. Then, I used a WHERE clause with OR to filter for employees in the Finance and Sales departments. The first condition is department = 'Finance', which filters for employees from the Finance department. The second condition is department = 'Sales', which filters for employees from the Sales department. Seventy-one total employee machines that needed updates were found. 

<br></br>

### Retrieving All Employees not in IT

In this scenario, the security team wanted to make final updates to all employee machines. The Information Technology department had already installed this update on all their employee machines, but employees in all other departments still required it. To retrieve a list of all employees that still required the update, I selected all data from the employees table via SELECT * FROM employees. Then, I used a WHERE clause with NOT to filter for employees not in the ‘Information Technology’  department

![image](https://github.com/user-attachments/assets/5007fae2-a56e-41eb-afac-83b79cfd1a50)

<br></br>

### Finding Login Attempts using Joins

For the final task, I investigated a security incident that had compromised some machines. First, I used an inner join to identify which employees were using which machines. Second, I used left and right joins to find machines that did not belong to any specific user and users with no specific machine assigned to them. Finally, I used an inner join to list all login attempts made by all employees.


The following demonstrates the inner join I used on the “machines” and “employees” tables to identify which employees were associated with which machines. I started by typing SELECT * FROM machines. After this, I used an INNER JOIN to link the two tables on the common column of device_id. 

![image](https://github.com/user-attachments/assets/f5ecfa76-04ae-4458-895b-f4f4e99e286e)


The second step was to (1) find information on all machines and the employees who have machines and (2) retrieve the information of all employees and the machines assigned to them. I achieved this by completing a left join on the two tables followed by a subsequent right join, as shown below.

![image](https://github.com/user-attachments/assets/e429ebc6-8c8b-4ab6-88e3-c3e1e7be262f)


In the right join, all records from the table referenced after <b>RIGHT JOIN</b> are included in the result. This included all records from the employees table, regardless of whether they had a machine assigned to them.

![image](https://github.com/user-attachments/assets/f0404473-9f32-4e99-b3f6-fb0df8b2fcc1)


The final task was to continue investigating the security incident by retrieving the information on all employees who made login attempts. To achieve this, I created an inner join on the employees and log_in_attempts tables, linking them with the username column.
The following screen capture demonstrates this input. 


![image](https://github.com/user-attachments/assets/760ac99a-a186-43da-8dbd-c826f0b08e71)

## Summary

In this simulation, I effectively applied filters and joins to SQL queries to retrieve information crucial for security analysis. I engaged with three  primary tables: 'log_in_attempts', ‘machines,’ and ‘'employees.' I utilized logical operators like AND, OR, and NOT to isolate specific data. Additionally, I employed the LIKE operator and the '%' wildcard to filter based on patterns. Lastly, I used various types of joins to retrieve associated data from different tables in one query. This approach enabled a successful extraction of data pertinent to login attempts and employee machine details across various scenarios.
