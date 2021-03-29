# README

## Abstract

#### 		This project is based on following elements:

#### 				1. Golang

#### 				2. Gin Framework

#### 				3. JWT(Json Web Token)

#### 				4. Restful API

#### 				5. Mongodb 

#### 		6. GCP(Google Cloud Platform)

#### 		7. GKE(Google Kubernetes Engine)

#### 		To build a simple todo list project, while using Postman to test all the API functionality. Additionally, one can build with Docker and push it to GKE and expose to the internet.

## Features

### 	1. users/singup : Post method

#### 		Sample input:

```json
{
  "user_id": "admin",
  "password": "88888888"
}
```

#### 		Sample output:

```json
{
  "InsertedID": "60581eb9cc2216b508d7477d"
}
```



### 	2. users/login : Post method

#### 		Sample input:

```json
{
  "user_id": "admin",
  "password": "88888888"
}
```

#### 		Sample output:

```json
{
  "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJVc2VyX2lkIjoiYWRtaW4iLCJleHAiOjE2MTY0NzQxNjl9.aAlh_LuxqLfWWSzCd3uA3C2RoBOTnC3HSqPaAvzYIkE"
}
```



### 	3. users/todo_list : Post method

#### 		Sample input:

```json
{
  "Authorization": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJVc2VyX2lkIjoiYWRtaW4iLCJleHAiOjE2MTY0NzQxNjl9.aAlh_LuxqLfWWSzCd3uA3C2RoBOTnC3HSqPaAvzYIkE",
  "todo_list": ["do homework", "write diary"]
}
```

#### 		Sample output:

```json
{
  "MatchedCount": 1,
  "ModifiedCount": 1,
  "UpsertedCount": 0,
  "UpsertedID": null
}
```



### 	4. User/todo_list : Get method

#### 		Sample input:

```json
{
  "Authorization": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJVc2VyX2lkIjoiYWRtaW4iLCJleHAiOjE2MTYxNzMyODZ9.8nri7jkBQPr-0ygZe5a8W2OB1K8TdmNJtc0W-XAqVkk
}
```

#### 		Sample output:

```json
[
  "do homework",
  "write diary"
]
```



### 	5. User/todo_list : Delete method

#### 		Sample input:

```json
{
  "Authorization": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJVc2VyX2lkIjoiYWRtaW4iLCJleHAiOjE2MTYxNzMyODZ9.8nri7jkBQPr-0ygZe5a8W2OB1K8TdmNJtc0W-XAqVkk",
  "delete_element": "do homework"
}
```

#### 	Sample output:

```json
{
  "MatchedCount": 1,
  "ModifiedCount": 1,
  "UpsertedCount": 0,
  "UpsertedID": null
}
```


##GCP + GKE

#### 	To build a docker file, first go to `/Todo_List`, and then type in the following command:

```dockerfile
docker build -t asia.gcr.io/PROJECT_ID/todo_list .
```

#### which will generate a image of this project.



#### 	To push the image to GCP, we type in the following command:

```
docker push asia.gcr.io/PROJECT_ID/todo_list
```

#### which just push the image file to your GCP project.



#### 	Now, to run the project o GKE, we use:

```
kubectl run todolist --image=asia.gcr.io/PROJECT_ID/todo_list
```

#### which tells GKE to run the project.



#### 	You can check if this is working by the following command:

```
kubectl get pods
```

#### this will give you the current state of your `pod`.



#### 	If the state is running, now you can enter the Docker by the following command:

```
kubectl exec -it todolist -- bash
```

#### which will let you get in the docker


#### 	Fianlly, to expose your project to Internet, use the following command:

```
kubectl expose deployment todolist-server --type LoadBalancer --port 80 --target-port 80
```

#### which specifies both the exposed port in docker and the port of your localhost are 80, and also generate a loadbalancer.



#### 	Now, use the following command to truely deploy the project:

```
kubectl create deployment todolist-server --image=asia.gcr.io/PROJECT_ID/todo_list
```

#### 

#### 	To get the ip of your project, use the following command:

```
kubectl get service
```

#### 	To delete the service, use:

```
tubectl delete service todolist-service
```

## 

## Postman

### Usage

#### In the repo, you can find `TodoList.postman_collection.json` and then import in the Postman.