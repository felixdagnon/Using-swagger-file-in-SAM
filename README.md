# Using-swagger-file-in-SAM
Using swagger file in SAM


We already create lambda as endpoint of API using SAM

![image](https://github.com/felixdagnon/Using-swagger-file-in-SAM/assets/91665833/67aa9157-310e-4152-862b-a7bf445a8a6a)

 we will be making changes to our code as per SAM specifications Swagger (https://swagger.io/)

Until now, we were creating our APIs directly. However, the right way to do it is to first Design your APIs and then Implement it.

Also, since APIs you create will be most likely consumed by others, it is better to design them in a standardized form. This is where 

Swagger comes into pictureSwagger is an open-source software framework that helps developers design, build, document, and consume 

RESTful Web services. It brings the whole ecosystem of standards, tools, specifications, best practices and people to help build best 

APIs possible. Here are the steps we will complete in this demo.

- Setup Project structure
  
- Design API with Swagger

- Integrate swagger file with Lambda functions

- Write code to implement Lambda functions

- Define deployment template as per SAM specs

- Deploy project using SAM template and CLI commands

- Verify all resources are created properly

- Testing of API

- Clean up

Let’s get started.

If we are difining the swagger file already created lambda, we can directly put in the url of lambda.

However if we are created lambda and API in the same SAM, the swagger file has to ingest the name of lambda from SAM

![image](https://github.com/felixdagnon/Using-swagger-file-in-SAM/assets/91665833/2af09993-7e2f-4276-99a0-b098a18f3c49)

# Sswagger with already created lambda

Here Sswagger pointing to preexisting lambda. If we are exporting swagger from API and API gateway and we have to recreate

API in other environment, then we have to use this.

We create a folder in cloud9 called APIfile and have swagger and preexisting lambda in it





