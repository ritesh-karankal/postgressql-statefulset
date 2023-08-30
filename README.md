# postgressql-statefulset

1. Access the PostgreSQL Database:

a. Open a terminal on your local machine.

b. Use the kubectl exec command to get inside the postgres-0 pod's shell:

sh
Copy code
kubectl exec -it postgres-0 -- /bin/bash
c. This command opens a shell inside the postgres-0 pod, allowing you to interact with its filesystem and execute commands.

2. Use the psql Command:

a. After executing the previous command, you'll find yourself inside the pod's shell.

b. To access the PostgreSQL database, use the psql command followed by the necessary arguments:

sh
Copy code
psql -U myuser mydb
Here, -U specifies the PostgreSQL user (myuser in your example) and mydb is the name of the database you want to connect to.

c. Once you hit Enter, you'll be prompted to enter the password for the specified user. Enter the password you set (mypassword in your example).

d. If everything is set up correctly, you'll be granted access to the PostgreSQL shell for the specified user and database.

3. Testing Data Persistence:

a. Once you're inside the PostgreSQL shell, you can create test data in the database.

b. For instance, you can create a simple table:

sql
Copy code
CREATE TABLE test_table (id SERIAL PRIMARY KEY, data TEXT);
c. Insert some data into the table:

sql
Copy code
INSERT INTO test_table (data) VALUES ('Hello, world!');
d. Query the data you inserted:

sql
Copy code
SELECT * FROM test_table;
e. Once you're done testing, you can exit the PostgreSQL shell:

sql
Copy code
\q
4. Exiting the Pod Shell:

a. To exit the pod's shell and return to your local terminal, simply type:

sh
Copy code
exit
This entire process allows you to interact with the PostgreSQL database inside the postgres-0 pod, verifying that the database is operational and that data persists across sessions. Remember, these steps are meant for testing and validation. In a production environment, you'd automate database initialization and data insertion, set up user authentication, and implement security measures to protect your database.


/Q why does it create a pod postgres-0 after deleting postgre-0 and not postgres-1/

When you delete a pod managed by a StatefulSet (e.g., postgres-0), the StatefulSet controller interprets it as a need to replace the pod. However, it doesn't create a new pod with a different ordinal index (e.g., postgres-1). Instead, it replaces the pod with the same ordinal index (postgres-0), ensuring that the hostname and identity remain consistent.
