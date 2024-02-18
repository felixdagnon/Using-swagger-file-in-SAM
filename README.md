# Using-swagger-file-in-SAM
Using swagger file in SAM


We already create lambda as endpoint of API using SAM

![image](https://github.com/felixdagnon/Using-swagger-file-in-SAM/assets/91665833/67aa9157-310e-4152-862b-a7bf445a8a6a)


AWS SAM (https://git.io/vb4O9)

This time, we will look at one more method for deploying serverless projects. It is called AWS Serverless Application Model or SAM

in short. AWS SAM is an open-source specification for deployment of serverless projects. It is like a domain specific deployment

language created by optimizing cloud formation templates further for serverless projects.

Because of this, you end up writing few lines of code of SAM template, which in turn gets converted into a lot more lines of code of c

loudformation template. However, SAM has specific opinions on your code structure should be, so we will be making changes to our code as 

per SAM specifications Swagger (https://swagger.io/)

Until now, we were creating our APIs directly. However, the right way to do it is to first Design your APIs and then Implement it.

Also, since APIs you create will be most likely consumed by others, it is better to design them in a standardized form. This is where 

Swagger comes into pictureSwagger is an open-source software framework that helps developers design, build, document, and consume 

RESTful Web services. It brings the whole ecosystem of standards, tools, specifications, best practices and people to help build best 

APIs possible. On 1st January 2016, the Swagger specification was renamed Open API Specification (https://www.openapis.org/). However 

we will refer to it as swagger. Here are the steps we will complete in this blog post.

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
