# Using-swagger-file-in-SAM
Using swagger file in SAM




Until now, we were creating our APIs directly. However, the right way to do it is to first Design your APIs and then Implement it.

Also, since APIs you create will be most likely consumed by others, it is better to design them in a standardized form. This is where 

Swagger comes into pictureSwagger is an open-source software framework that helps developers design, build, document, and consume 

RESTful Web services. It brings the whole ecosystem of standards, tools, specifications, best practices and people to help build best 

APIs possible.

 we will be making changes to our code as per SAM specifications Swagger


We already create lambda as endpoint of API using SAM

![image](https://github.com/felixdagnon/Using-swagger-file-in-SAM/assets/91665833/67aa9157-310e-4152-862b-a7bf445a8a6a)


If we are difining the swagger file already created lambda, we can directly put in the url of lambda.

However if we are created lambda and API in the same SAM, the swagger file has to ingest the name of lambda from SAM

![image](https://github.com/felixdagnon/Using-swagger-file-in-SAM/assets/91665833/2af09993-7e2f-4276-99a0-b098a18f3c49)


Let’s get started.

 Here are the steps we will complete in this demo.

- Swagger with already created lambda

- Creating API with Swagger and new lambda in SAM


# Swagger with already created lambda

Here Sswagger  with url of AI gateway pointing to preexisting lambda. If we are exporting swagger from API and API gateway and we have to recreate

API in other environment, then we have to use this.

Previously, I export swagger file from API gateway stage "GreatfromCountry " I have created

```json
swagger: "2.0"
info:
  version: "2024-01-31T11:07:13Z"
  title: "GreatfromCountry"
host: "4ipt1ltbz5.execute-api.us-east-1.amazonaws.com"
basePath: "/Dev"
schemes:
- "https"
paths:
  /:
    get:
      consumes:
      - "application/json"
      produces:
      - "application/json"
      parameters:
      - name: "nameofCountry"
        in: "query"
        required: true
        type: "string"
      responses:
        "200":
          description: "200 response"
          schema:
            $ref: "#/definitions/Empty"
      x-amazon-apigateway-integration:
        type: "aws"
        httpMethod: "POST"
        uri: "arn:aws:apigateway:us-east-1:lambda:path/2015-03-31/functions/arn:aws:lambda:us-east-1:944020312758:function:GreatFromCountry/invocations"
        responses:
          default:
            statusCode: "200"
        requestTemplates:
          application/json: " {\"Country\":\"$input.params('nameofcountry')\"}"
        passthroughBehavior: "when_no_templates"
        cacheNamespace: "5q1e91vlab"
        cacheKeyParameters:
        - "method.request.querystring.nameofCountry"
        contentHandling: "CONVERT_TO_TEXT"
definitions:
  Empty:
    type: "object"
    title: "Empty Schema"
```

We create a folder in cloud9 called APIfile and have swagger and preexisting lambda in it.

![image](https://github.com/felixdagnon/Using-swagger-file-in-SAM/assets/91665833/198222f0-90ac-41f3-a3ed-75ebd23ddff7)

# Create swagger preexisting lambda template with SAM

Let's run this package swagger-preexisting-lambda.yml:

$ sam package --template-file swagger-preexisting-lambda.yml --s3-bucket demotest-101 --output-template-file swagger-preexisting-lambda-packaged.yml

The pacckage is downloaded in SAM folder of Cloud9

![image](https://github.com/felixdagnon/Using-swagger-file-in-SAM/assets/91665833/92acd7ff-8049-4a4a-b183-8a6951f99bc3)

It take the code from local directory and put it in s3 bucket.

Let's check s3 bucket

![image](https://github.com/felixdagnon/Create-API-and-lambda-events-using-SAM/assets/91665833/6338f502-f995-48cb-8617-3e459dca00e4)


# Deploying swagger preexisting lambda package with SAM

To deploy the package run the below command

$ sam deploy --template-file swagger-preexisting-lambda-packaged.yml --stack-name SAM-API-Swagger-1 --capabilities CAPABILITY_IAM

The package is done and changeset created in cloudformation

![image](https://github.com/felixdagnon/Using-swagger-file-in-SAM/assets/91665833/24981ccb-9523-45bd-a69a-f68b02fb1fb9)

Let's see Cloudformation. The stack is created

![image](https://github.com/felixdagnon/Using-swagger-file-in-SAM/assets/91665833/e8e5a9ce-ebcd-4cf0-a9f6-f3ddfc9e5d89)

Let's check out API Gateway 

![image](https://github.com/felixdagnon/Using-swagger-file-in-SAM/assets/91665833/039be525-f2db-4229-ab16-599489fad858)

It's pointing lambda function

![image](https://github.com/felixdagnon/Using-swagger-file-in-SAM/assets/91665833/39bf4d40-a0ae-4d7b-ac1c-84acfdf0d5c8)

Let's check query string in method request. It's caching

![image](https://github.com/felixdagnon/Using-swagger-file-in-SAM/assets/91665833/7c0b5509-e110-4ad4-bcef-b98706272de4)

Let's check query string in integration request. It's grabbing "naofCountry" from url and passe Country to lambda

![image](https://github.com/felixdagnon/Using-swagger-file-in-SAM/assets/91665833/5ef879ca-7b76-42a6-9c93-4811585e39dc)


# Creating API with Swagger and new lambda in SAM

The most difference here, we will give the name of lambda function in swagger template. Previouly, we let SAM give idendical name to the function.

Here lambda will generated exactely the same name. We do not use arn of lambda in swagger template


![image](https://github.com/felixdagnon/Using-swagger-file-in-SAM/assets/91665833/bece4023-cc77-4244-a859-81b200f53cd9)


Let's run this package swagger-SAMcreated-lambda.yml:

$ sam package --template-file swagger-SAMcreated-lambda.yml --s3-bucket demotest-101 --output-template-file swagger-SAMcreated-lambda-packaged.yml

The pacckage is downloaded in SAM folder of Cloud9

![image](https://github.com/felixdagnon/Using-swagger-file-in-SAM/assets/91665833/92acd7ff-8049-4a4a-b183-8a6951f99bc3)

It take the code from local directory and put it in s3 bucket.

Let's check s3 bucket

![image](https://github.com/felixdagnon/Create-API-and-lambda-events-using-SAM/assets/91665833/6338f502-f995-48cb-8617-3e459dca00e4)


# Deploying swagger preexisting lambda package with SAM

To deploy the package run the below command

$ sam deploy --template-file swagger-preexisting-lambda-packaged.yml --stack-name SAM-API-Swagger-1 --capabilities CAPABILITY_IAM

The package is done and changeset created in cloudformation

![image](https://github.com/felixdagnon/Using-swagger-file-in-SAM/assets/91665833/24981ccb-9523-45bd-a69a-f68b02fb1fb9)

Let's see Cloudformation. The stack is created

![image](https://github.com/felixdagnon/Using-swagger-file-in-SAM/assets/91665833/e8e5a9ce-ebcd-4cf0-a9f6-f3ddfc9e5d89)

Let's check out API Gateway 

![image](https://github.com/felixdagnon/Using-swagger-file-in-SAM/assets/91665833/039be525-f2db-4229-ab16-599489fad858)

It's pointing lambda function

![image](https://github.com/felixdagnon/Using-swagger-file-in-SAM/assets/91665833/39bf4d40-a0ae-4d7b-ac1c-84acfdf0d5c8)

Let's check query string in method request. It's caching

![image](https://github.com/felixdagnon/Using-swagger-file-in-SAM/assets/91665833/7c0b5509-e110-4ad4-bcef-b98706272de4)

Let's check query string in integration request. It's grabbing "naofCountry" from url and passe Country to lambda

![image](https://github.com/felixdagnon/Using-swagger-file-in-SAM/assets/91665833/5ef879ca-7b76-42a6-9c93-4811585e39dc)














