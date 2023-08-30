# Deploying PostgreSQL on Kubernetes using a StatefulSet

Let's understand some terms first (don't overwhelm yourself with the term and new things introduced just try to understand what they are doing)

### 🎥 Resources 
- [Brief about components](https://youtu.be/Krpb44XR0bk?si=Ws-FRFg9GSUMFEZV)
- [Statefulset](https://youtu.be/Vrxr-7rjkvM?si=wjOlICkt78X2aEGa)
- [Service](https://youtu.be/T4Z7visMM4E?si=fdCjBkNU3GxqfDW9)
- [Persistent Volume & claim](https://youtu.be/0swOh5C3OVM?si=uQ8zCszBXvZ2Ag8l)
- [Blog](https://kodekloud.com/blog/deploy-postgresql-kubernetes/#deploying-postgres-as-a-stateful-set-with-a-headless-service)
- techworld with Nana and KodeKloud is great youtube channel to learn about any concept. (feel free to look for other videos)

### ⚙️ Requirements
  - you will need a local kubernetes cluster
  
  - Install minikube from here - https://minikube.sigs.k8s.io/docs/start/ (check commands which in the box curl...)

Start minikube (you will see some pretty emojis have patience it will take time)
```
minikube start
```
and check pods with
```
kubectl get po -A
```
![image](https://github.com/ritesh-karankal/postgressql-statefulset/assets/71586008/e8ba456a-d449-491c-bb25-abd9b5a47091)


### 👉 Steps
Now you have to read this [blog](https://kodekloud.com/blog/deploy-postgresql-kubernetes/#deploying-postgres-as-a-stateful-set-with-a-headless-service) till the ```"Deploying Postgres as a Stateful Set with a Headless Service"``` topic but follow the step mentioned below and use the file/yaml manifest from this repo (Just focus on going through the blog and the commands in this readme to acheive the goal we are trying to do after that we can understand how things are working)

Here's a step-by-step guide to deploying PostgreSQL on Kubernetes using a StatefulSet:
### ⭐️ [If you downloaded this repo the file already (You have completed steps 1 to step 3) you can now jump to step 4]
But if you want to create this manifests on your own using the terminal, follow these steps:

### Step 1: Create a Persistent Volume (PV) and Persistent Volume Claim (PVC):
First, you need to define the storage that PostgreSQL will use. This involves creating a Persistent Volume and a Persistent Volume Claim to bind to it.

1. Open a text editor and paste the YAML content from [here]() into a new file, for example, named postgres_pv_and_pvc.yaml.

2. Save the file.

3. Open a terminal window.

4. Navigate to the directory where you saved the YAML file using the cd command.

  Run the following command to apply the manifest to your Minikube cluster:

```
kubectl apply -f postgres-manifest.yaml
```
![image](https://github.com/ritesh-karankal/postgressql-statefulset/assets/71586008/ee1359aa-b10e-45cc-adda-d5a3215dd219)

You can verify them by running:
```
kubectl get pv
kubectl get pvc
```
![image](https://github.com/ritesh-karankal/postgressql-statefulset/assets/71586008/c67c9f6c-7050-4614-a480-f39b4fd866c7)

### Step 3: Deploy PostgreSQL StatefulSet:
Create a StatefulSet manifest to deploy PostgreSQL. Here's a simplified version:
1. Open a text editor and paste the YAML content from [here]() into a new file, for example, named postgres_pv_and_pvc.yaml.

![image](https://github.com/ritesh-karankal/postgressql-statefulset/assets/71586008/3f46c1e0-a262-4843-b99f-cfd9b001a99e)

2. Save the file.

3. Open a terminal window.

4. Navigate to the directory where you saved the YAML file using the cd command.

  Run the following command to apply the manifest to your Minikube cluster:

```
kubectl apply -f postgres-manifest.yaml
```

![image](https://github.com/ritesh-karankal/postgressql-statefulset/assets/71586008/4c3bdf07-3ab5-493f-afca-98b4101e3bd2)

The command above will create the headless service and the stateful set in your cluster. You can verify them by running:
```
kubectl get svc
kubectl get sts
kubectl get pods
kubectl get pvc -l app=postgres
```
![image](https://github.com/ritesh-karankal/postgressql-statefulset/assets/71586008/297f9193-b27c-46af-8ff5-ceefbc81ee30)


### Step 4: Apply the Configurations (if you downloaded the files):
Apply the configurations by running:

```
kubectl apply -f pv_and_pvc.yaml
kubectl apply -f configmap.yaml
kubectl apply -f statefulset.yaml
```

### Step 5: Accessing PostgreSQL:
To access the PostgreSQL instance, follow this file - [statefulset](statefulset.md)
