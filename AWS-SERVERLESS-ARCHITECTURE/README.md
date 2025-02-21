# AWS-Serverless-Architecture




AWS serverless architecture is a cutting-edge paradigm that optimizes scalability, flexibility, and cost-effectiveness in application development. In my architectural flow, I leverage key serverless services offered by AWS, namely AWS Lambda, DynamoDB, and API Gateway, to streamline CRUD (Create, Read, Update, Delete) operations on a DynamoDB database

AWS Lambda allows me to execute code without the need for provisioning or managing servers, enabling efficient, event-driven computing. DynamoDB serves as a serverless NoSQL database, providing seamless scalability and low-latency performance.



![a1](https://github.com/SarKaushik/Advanced-SQL-Database-Project-/assets/85201993/8faa45c6-8630-4371-ace3-d6126594a8c3)
    


API Gateway facilitates the creation of secure and scalable APIs, ensuring seamless communication between the client application and the backend services. This serverless stack not only simplifies infrastructure management but also enhances agility and responsiveness, delivering a cost-effective and high-performance solution for CRUD operations and result presentation to end-users.





**Create Policy:**
Create a lambda AWS customer-managed policy to attach to your lambda role.


![createpolicy](https://github.com/SarKaushik/Advanced-SQL-Database-Project-/assets/85201993/9e15d7a9-85b4-4083-9985-397485f34966)



Create Role for Lambda Fucntion
Created a role for the lambda function and attached a specific lambda policy to the role.
Lamda's role would enable Cloud watch and Dynamo DB operations for the lambda function.


![CREATE POLICY](https://github.com/SarKaushik/AWS-Serverless-Architecture-/assets/85201993/b9d762f2-f280-415f-ab2b-31be665646de)



{
"Version": "2012-10-17",
"Statement": [
{
  "Sid": "Stmt1428341300017",
  "Action": [
    "dynamodb:DeleteItem",
    "dynamodb:GetItem",
    "dynamodb:PutItem",
    "dynamodb:Query",
    "dynamodb:Scan",
    "dynamodb:UpdateItem"
  ],
  "Effect": "Allow",
  "Resource": "*"
},
{]\\]]\]-kjnnerKJ
  "Sid": "",
  "Resource": "*",
  "Action": [
    "logs:CreateLogGroup",
    "logs:CreateLogStream",
    "logs:PutLogEvents"
  ],
  "Effect": "Allow"
}
]
}


**Lambda Function:**
AWS Lambda is a serverless computing service provided by Amazon Web Services (AWS). It allows developers to run code without provisioning or managing servers, automatically scaling based on the incoming request traffic. Lambda functions are small, stateless, and event-driven units of computation that can be written in various programming languages, including Node.js, Python, Java, and more. 

Lambda is connected to API Gateway for trigger events, as soon as API Gateway invokes the lambda function, it triggers an operation to the Dynamo DB database.


![LAMBDA FUNCTION](https://github.com/SarKaushik/AWS-Serverless-Architecture-/assets/85201993/ae4546ab-e7a6-4711-a2d1-f3d5ae949eea)



**Code:**


from __future__ import print_function

import boto3
import json

print('Loading function')


def lambda_handler(event, context):
    '''Provide an event that contains the following keys:

      - operation: one of the operations in the operations dict below
      - tableName: required for operations that interact with DynamoDB
      - payload: a parameter to pass to the operation being performed
    '''
    #print("Received event: " + json.dumps(event, indent=2))

    operation = event['operation']

    if 'tableName' in event:
        dynamo = boto3.resource('dynamodb').Table(event['tableName'])

    operations = {
        'create': lambda x: dynamo.put_item(**x),
        'read': lambda x: dynamo.get_item(**x),
        'update': lambda x: dynamo.update_item(**x),
        'delete': lambda x: dynamo.delete_item(**x),
        'list': lambda x: dynamo.scan(**x),
        'echo': lambda x: x,
        'ping': lambda x: 'pong'
    }

    if operation in operations:
        return operations[operation](event.get('payload'))
    else:
        raise ValueError('Unrecognized operation "{}"'.format(operation))





**Dynamo DB Table**

DynamoDB, part of Amazon Web Services, is a fully managed NoSQL database service. A DynamoDB table is a schema-less data container offering seamless scalability and consistent, low-latency performance. It supports automatic scaling and different capacity modes. 

Users define primary keys for efficient data retrieval, and the service provides built-in security features. DynamoDB tables are ideal for various applications due to their high availability, durability, and hassle-free management.

Created Dynamo DB database to store and retrieve necessary data elements. 
![Dynamo DB Table](https://github.com/SarKaushik/AWS-Serverless-Architecture-/assets/85201993/44ffcb63-952d-4c07-8d0c-72eeb5f68227)



**API Gateway**

Amazon API Gateway is a fully managed service by Amazon Web Services that enables the creation, management, and deployment of APIs at scale. It acts as a gateway between applications and backend services, allowing developers to create, publish, and secure APIs with ease. 

With features like authentication, authorization, and traffic management, API Gateway simplifies the process of building robust and scalable APIs, facilitating seamless integration with other AWS services and external endpoints. It also supports the creation of custom domain names for APIs, enhancing branding and accessibility.

Created resources and methods for Rest API gateway to trigger lambda function and perform specific operations on Dynamo DB database through lambda function.
![API Gateway](https://github.com/SarKaushik/AWS-Serverless-Architecture-/assets/85201993/d1b4b4f3-0890-498f-b9d0-a2e690dff235)











**Postman:**

![postman](https://github.com/SarKaushik/AWS-Serverless-Architecture-/assets/85201993/8bd52f2f-5c5f-4a64-ab6e-430b741f7ca4)


Postman is a popular API development and testing tool that simplifies the process of designing, testing, and documenting APIs. With a user-friendly interface, developers can easily create and send HTTP requests, analyze responses, and collaborate on API development. Postman supports various authentication methods, automates testing workflows, and allows the organization of requests into collections for better management. It is widely used for API exploration, testing, and monitoring, making it an essential tool for developers and teams working on API-driven projects.

Utilized Postman tool to test API gateway by sending create, read, update, and delete commands to trigger lambda function to perform CRUD operations on dynamo db database.



{
    "operation": "create",
    "tableName": "lambda-apigateway",
    "payload": {
        "Item": {
            "id": "2377ab",
            "number": 4
        }
    }
}


{
    "operation": "read",
    "tableName": "lambda-apigateway",
    "payload": {
        "Key": {
            "id": "127748AB"
        }
    }
}


{
    "operation": "update",
    "tableName": "lambda-apigateway",
    "payload": {
        "Key": {
            "id": "127748AB"
        },
        "UpdateExpression": "SET attributeName = :newValue",
        "ExpressionAttributeValues": {
            ":newValue": "674899B"
        }
    }
}


{
    "operation": "update",
    "tableName": "lambda-apigateway",
    "payload": {
        "Key": {
            "id": "127748AB"
        },
        "UpdateExpression": "SET FirstName = :newValue",
        "ExpressionAttributeValues": {
            ":newValue": "Sarvesh"
        }
    }
}



{
    "operation": "update",
    "tableName": "lambda-apigateway",
    "payload": {
        "Key": {
            "id": "127748AB"
        },
        "UpdateExpression": "SET LastName = :newValue",
        "ExpressionAttributeValues": {
            ":newValue": "Kaushik"
        }
    }
}


{
    "operation": "delete",
    "tableName": "lambda-apigateway",
    "payload": {
        "Key": {
            "id": "127748AD"
        }
    }
}













