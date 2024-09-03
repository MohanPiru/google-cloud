# Deploying a Python Flask webapp in App Engine in Google Cloud

Deployed my System-monitoring flask webapp in Google cloud app Engine

## App Engine
* **Serverless:** You don't need to manage servers. App Engine handles it for you. It is a platform as a service (Paas) offered by Google Cloud.

* **Scalable:** App Engine automatically scales your application to handle traffic.

* **supported language** Python, Java, Go, PHP, Node.js, .NET

* App Engine integrates smoothly with Google Cloud services like Cloud SQL, Cloud Storage, Firestore, Pub/Sub, and more, making it easier to build and scale complex applications.

### Important Points 
* each Google Cloud project can have only one App Engine application

* You can create manual versions by explicitly specifying a version name.

```
 gcloud app deploy -v v1 
 ```

* By default all the traffic is send to new version after deployed. If you dont need just run the command with the following tag. Can also split traffic between versions.

```
gcloud app deploy -v v2 --no-promote
```

## My Application
* First make sure **App Engine Admin API** is enable for your project.

* create an app engine **application** (select an region and a service account (can choose default))

 * Clone your git repo
   ```
   git clone https://github.com/MohanPiru/system-monitoring.git
   ```
* By default app engine install all required modules/dependencies defined in **requirements.txt** file.

* you have to add one extra file that is **app.yaml** By default app engine install the runtime specified in this file also it acts as a descriptor for its deployment. 

  my app.yaml file looks like -->>
  ```
   runtime: python39 

   entrypoint: gunicorn -b :$PORT app:app
   ```

  If your python file name is **main.py** then you dont need to add the 2nd line.
  Google App Engine assumes that the default Python file for your application is **main.py**. 

  Now my `entrypoint` is pointing to the `app.py` 
* Just run gcloud command of app engine
  ``` gcloud app deploy -v v1 ```

* Now run `gcloud app browse ` to get the link of the application.

![Screenshot (19)](https://github.com/user-attachments/assets/147a18cf-7372-43af-b30a-a0066c30f97a)


