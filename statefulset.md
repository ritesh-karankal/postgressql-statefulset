# postgressql-statefulset

Resources from the previous file -
- [Blog](https://kodekloud.com/blog/deploy-postgresql-kubernetes/#deploying-postgres-as-a-stateful-set-with-a-headless-service)
- [Statefulset](https://youtu.be/Vrxr-7rjkvM?si=Aun1541VjnVmTCHl)

Great Job!!
The postgres-0 pod you have created is the initial pod in your StatefulSet, and it's running an instance of the PostgreSQL database. 
You can see it by command
```
kubectl get po -A
```
![image](https://github.com/ritesh-karankal/postgressql-statefulset/assets/71586008/a50c17bc-7b95-406a-a81f-240fbddc3d1b)


The following process allows you to interact with the PostgreSQL database inside the postgres-0 pod, verifying that the database is operational and that data persists across sessions. 

## ⭐ Our goal is to check when you delete postgres-0 pod, a new pod with the same name (postgres-0) will be created by the StatefulSet to replace the deleted pod.

/Q If I delete the postgressql pod the data still persists? 

/A In Kubernetes, the data will persist even if you delete the PostgreSQL pod. This persistence is due to the combination of the StatefulSet and the PersistentVolumeClaim (PVC) configurations you've set up.


### 1. Access the PostgreSQL Database:

  a. Open a terminal on your local machine.
  
  b. Use the kubectl exec command to get inside the postgres-0 pod's shell:
  
  ```
  kubectl exec -it postgres-0 -- /bin/bash
  ```
  c. This command opens a shell inside the postgres-0 pod, allowing you to interact with its filesystem and execute commands.

### 2. Use the psql Command:

  a. After executing the previous command, you'll find yourself inside the pod's shell.
  
  b. To access the PostgreSQL database, use the psql command followed by the necessary arguments:
  
  ```
  psql -U myuser mydb
  ```
  Here, -U specifies the PostgreSQL user (myuser in your example) and mydb is the name of the database you want to connect to.
  
  c. Once you hit Enter, you'll be prompted to enter the password for the specified user. Enter the password you set (mypassword in your example).
  
  d. If everything is set up correctly, you'll be granted access to the PostgreSQL shell for the specified user and database.

### 3. Create Data:

  a. Once you're inside the PostgreSQL shell, you can create test data in the database.
  
  b. For instance, you can create a simple table:
  
  ```
  CREATE TABLE test_table (id SERIAL PRIMARY KEY, data TEXT);
  ```
  c. Insert some data into the table:
  
  ```
  INSERT INTO test_table (data) VALUES ('Hello, world!');
  ```
  d. Query the data you inserted:
  
  ```
  SELECT * FROM test_table;
  ```
  e. Once you're done testing, you can exit the PostgreSQL shell:
  
  ```
  \q
  ```
### 4. Exiting the Pod Shell:

  a. To exit the pod's shell and return to your local terminal, simply type:
  
  ```
  exit
  ```
### 5. Test Data Persistence

You can delete a pod managed by a StatefulSet using the ```kubectl delete command```. When you delete a pod managed by a StatefulSet, the StatefulSet controller will automatically create a new pod to maintain the desired replica count.

To delete a pod:

Open a terminal.

Run the following command to delete the pod:

```
kubectl delete pod <pod-name>
```
Replace <pod-name> with the name of the pod you want to delete. For example, if you want to delete postgres-0, the command would be:

```
kubectl delete pod postgres-0
```
Kubernetes will delete the specified pod. The StatefulSet controller will detect the missing pod and create a new one to replace it, ensuring that the desired replica count is maintained.


/Q why does it create a pod postgres-0 after deleting postgre-0 and not postgres-1/

When you delete a pod managed by a StatefulSet (e.g., postgres-0), the StatefulSet controller interprets it as a need to replace the pod. However, it doesn't create a new pod with a different ordinal index (e.g., postgres-1). Instead, it replaces the pod with the same ordinal index (postgres-0), ensuring that the hostname and identity remain consistent. As we saw in the video about statefulset that the master was postgres-0 and other slave pods will be pointing to it so, the name would be consistent.
