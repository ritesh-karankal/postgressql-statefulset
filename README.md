
Let's understand some terms first (don't overwhelm yourself with the term and new things introduced just try to understand what they are doing)
- [Brief about components](https://youtu.be/Krpb44XR0bk?si=Ws-FRFg9GSUMFEZV)
- [Statefulset](https://youtu.be/Vrxr-7rjkvM?si=wjOlICkt78X2aEGa)
- [Service](https://youtu.be/T4Z7visMM4E?si=fdCjBkNU3GxqfDW9)
- [Persistent Volume & claim](https://youtu.be/0swOh5C3OVM?si=uQ8zCszBXvZ2Ag8l)
- [Blog](https://kodekloud.com/blog/deploy-postgresql-kubernetes/#deploying-postgres-as-a-stateful-set-with-a-headless-service)
- techworld with Nana and KodeKloud is great youtube channel to learn about any concept. (feel free to look for other videos)

Now you have to follow this [blog](https://kodekloud.com/blog/deploy-postgresql-kubernetes/#deploying-postgres-as-a-stateful-set-with-a-headless-service) till the ```"Deploying Postgres as a Stateful Set with a Headless Service"``` topic but use the file/yaml manifest from this repo

(Just focus on following the blog and the commands in this readme to acheive the goal we are trying to do 
after that we can understand how things are working)

Here's a step-by-step guide to deploying PostgreSQL on Kubernetes using a StatefulSet:

### Step 1: Create a Persistent Volume (PV) and Persistent Volume Claim (PVC):
First, you need to define the storage that PostgreSQL will use. This involves creating a Persistent Volume and a Persistent Volume Claim to bind to it.


### Step 4: Apply the Configurations:
Apply the configurations by running:

```
kubectl apply -f pv_and_pvc.yaml
kubectl apply -f configmap.yaml
kubectl apply -f statefulset.yaml
```

### Step 5: Accessing PostgreSQL:
To access the PostgreSQL instance, follow this file - [statefulset](statefulset.md)
