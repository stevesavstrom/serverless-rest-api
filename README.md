# AWS Serverless REST API built

Example of a serverless REST API built with AWS. This API provides create, read, update, and delete (CRUD) functionality.

## Overview of AWS Services:
- [Lambda](https://aws.amazon.com/lambda/)
- [API Gateway](https://aws.amazon.com/api-gateway/)
- [DynamoDB](https://aws.amazon.com/dynamodb/)

## Prerequisites:
- [AWS account](https://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/) for provisioning services.
- Basic [Postman](https://learning.postman.com/docs/getting-started/introduction/) skills for testing the API.
- JavaScript and Node.js skills for writing the Lambda function.

## Steps:
- Create DynamoDB table
- Create Lambda function
- Create API Gateway resource and HTTP methods
- Test in Postman

## API Endpoints

Health Check
```
https://www.jetbrains.com/help/
```
Contacts
```
https://www.jetbrains.com/help/
```
Contact
```
https://www.jetbrains.com/help/
```

## Sample Requests
Delete a single contact in the database

Request
```
{
    "contactId": "10001",
}
```
Response
```
{
    "Operation": "DELETE",
    "Message": "SUCCESS",
    "Item": {
        "Attributes": {
            "firstName": "999",
            "lastName": "150",
            "email": "red",
            "phoneNumber": "10001",
        }
    }
}
```
