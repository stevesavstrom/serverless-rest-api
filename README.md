# AWS Serverless REST API
Example of a serverless REST API built with Amazon Web Services. This API provides create, read, update, and delete (CRUD) functionality.

- [Lambda](https://aws.amazon.com/lambda/)
- [API Gateway](https://aws.amazon.com/api-gateway/)
- [DynamoDB](https://aws.amazon.com/dynamodb/)

# Prerequisites
- [AWS account](https://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/) for provisioning cloud services.
- [Postman](https://learning.postman.com/docs/getting-started/introduction/) for testing the API.

# Create DynamoDB table
First create a new DynamoDB table. This will be the data source for the API.
1. Login to the AWS console using an IAM user.
2. Search for `DynamoDB`.
3. Click `Create table`.
4. Enter a table name such as `contact-list`.
5. Enter a partition key such as `contactId` with a data type of `String` (leave sort key blank for this example.)
6. Leave `Table settings` as `Default settings`.
7. Click `Create table`.

# Create an IAM role
Next, create an IAM role 

# Create Lambda function
Text

# Create API Gateway resource and HTTP methods
Text

# Test API Endpoints in Postman

## GET /health
Request Body:
```json
"None"
```
Response:
```json
"200 OK"
```
## GET /contacts
Request Body:
```json
"None"
```
Response:
```json
"200 OK"
```

## POST /contact
Request Body:
```json
{
	"occupation": "Dentist",
	"contactId": "10004",
	"lastName": "Smith",
	"email": "louis.smith@gmail.com",
	"phone": "505-426-8570",
	"firstName": "Louis"
}
```
Response:
```json
{
    "Operation": "SAVE",
    "Message": "SUCCESS",
    "Item": {
        "occupation": "Dentist",
        "contactId": "10004",
        "lastName": "Smith",
        "email": "louis.smith@gmail.com",
        "phone": "505-426-8570",
        "firstName": "Louis"
    }
}
```

## GET /contact?contactId=10004
Request Body:
```json
"None"
```
Response:
```json
{
	"contacts": [
		{
			"occupation": "Designer",
			"contactId": "10003",
			"lastName": "Smith",
			"email": "louis.smith@gmail.com",
			"phone": "505-426-8570",
			"firstName": "Louis"
		},
		{
			"occupation": "Designer",
			"contactId": "10002",
			"lastName": "Henson",
			"email": "stacy.henson@hotmail.com",
			"phone": "443-455-0735",
			"firstName": "Stacy"
		},
		{
			"occupation": "Software Engineer",
			"contactId": "10001",
			"lastName": "Neely",
			"email": "stephen.neely@yahoo.com",
			"phone": "803-740-4478",
			"firstName": "Stephen"
		}
	]
}
```

## PATCH /contact
Request Body:
```json
{
    "contactId": "10002",
    "updateKey": "phone",
    "updateValue": "612-999-9903"
}
```
Response:
```json
{
    "Operation": "UPDATE",
    "Message": "SUCCESS",
    "UpdatedAttributes": {
        "Attributes": {
            "phone": "612-999-0000"
        }
    }
}
```

## DELETE /contact
Request Body:
```json
{
    "contactId": "10004"
}
```
Response:
```json
{
    "Operation": "DELETE",
    "Message": "SUCCESS",
    "Item": {
        "Attributes": {
            "occupation": "Dentist",
            "contactId": "10004",
            "lastName": "Smith",
            "email": "louis.smith@gmail.com",
            "phone": "505-426-8570",
            "firstName": "Louis"
        }
    }
}
```
