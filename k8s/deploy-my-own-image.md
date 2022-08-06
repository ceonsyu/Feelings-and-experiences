---
description: create a deployment with local docker image
---
I have an application--[xgboost-serving](https://github.com/iqiyi/xgboost-serving), I builded it according to the guide of developers. After that, I have an image on my docker:
![xgboost-serving image](figures/截屏2022-08-05%20下午6.37.52.png)
## Step 1 Push Image
Before this step, It is needed to explain about building an application, It is something about build our code under Linux OS, make a Dockerfile and so on, I am not pretty sure about the whole procedure right now, hope I can figure it out someday.  
In order to create a deployment with my own image, I need to push this image to **Docker Hub**, a docker account is needed in this step:
```shell
# tag image
docker tag xgboost-serving qinshunong/xgboost-serving:v1.2.1-jdos
# push imgae
docker push qinshunong/xgboost-serving:v1.2.1-jdos
```
And there it is:
![docker hub](figures/截屏2022-08-05%20下午11.55.12.png)
## Step 2 Make Ymal file
Today I just used an `ymal` file like:
```yml
apiVersion: apps/v1

kind: Deployment

metadata:

  name: xgboost-deployment

spec:

  selector:

    matchLabels:

      app: xgboost-serving

  replicas: 2 # tells deployment to run 2 pods matching the template

  template:

    metadata:

      labels:

        app: xgboost-serving

    spec:

      containers:

        - name: xgboost-serving

          image: qinshunong/xgboost-serving:v1.2.1-jdos

          ports:

            - containerPort: 80
```
I use this `ymal` file in my java application which was recorded in [access-clusters-Java&HTTP](access-clusters-Java&HTTP.md) and run a POST method, it worked:
```shell
~ kubectl get deployments.apps
NAME                 READY   UP-TO-DATE   AVAILABLE   AGE
xgboost-deployment   2/2     2            2           5h33m
~ kubectl get po
NAME                                READY   STATUS    RESTARTS         AGE
xgboost-deployment-98485686-dd74w   1/1     Running   25 (6m14s ago)   5h33m
xgboost-deployment-98485686-lg9kc   1/1     Running   25 (6m18s ago)   5h33m
```
## Next
I will find a way to deploy a model file of xgboost to my xgboost deployment, and output prediction, like:
```shell
call predict ok
outputs size is 1
the result tensor[0] is:
54 57 42 59 42 58 39 41 52 41 53 58 47 58 54 60 36 57 60 50 40 41 54 57 48 43 31 58 60 31 62 47 47 52 58 40 44 53 54 53 42 31 40 36 56 54 61 60 31 51 61 48 42 59 31 51 33 62 49 60 38 52 35 44 40 56 32 58 61 51 58 52 46 22 33 33 31 57 33 56 49 39 56 52 49 61 36 49 48 39 31 44 31 46 32 33 56 56 40 53 51 31 31 31 62 39 39 38 35 56
Done.
```