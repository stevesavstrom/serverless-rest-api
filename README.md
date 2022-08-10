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
- Login to the AWS console using an IAM user.
- Search for `DynamoDB`.
- Click `Create table`.
- Enter a table name such as `contact-list`.
- Enter a partition key such as `contactId` with a data type of `String` (leave sort key blank for this example.)
- Leave `Table settings` as `Default settings`.
- Click `Create table`.

# Create Lambda function and attach IAM role and policies
- Search for `Lambda` in AWS Console.
- Click `Create function`
- Enter a function name such as `serverlessRestApi`.
- Select `Node.js` as a runtime.
- Under `Permissions` select `Change default execution role` and then `Create a new role from AWS policy templates` with a name such as `serverlessApiRole`.
- Click `Create function`.
- Click `Permissions` and then click on the role name that was just created.
- Click `Attach policies` and search for `CloudWatchLogsFullAccess`, select the policy, then click `Attach policy`.
- Click `Attach policies` and search for `DynamoDBFullAccess`, select the policy, then click `Attach policy`.

# Create API Gateway resource and HTTP methods
- Search for `API Gateway` in AWS Console.
- Click `Create API`.
- Go to `REST API` and click `Build`.
- Select `REST` and `New API`.
- Enter a name such as `contactListRestAPI` and leave endpoint type as `Regional`

## Creating a `/health` endpoint:

- Click `Actions` and then `Create resource`.
- Enter resource name `health` and select `Enable API Gateway CORS`.
- Select the `Health` resource and then click `Actions` and `Create method`.
- Select `GET` method with `Integration type` as `Lambda`
- Select `Use Lambda Proxy integration`.
- Select the deployment region where the Lambda function will be deployed as `us-east-1`.
- Search for the Lambda function by name such as `serverlessRestApi`.

## Creating a `/contacts` endpoint:

- Click `Actions` and then `Create resource`.
- Enter resource name `contacts` and select `Enable API Gateway CORS`.
- Select the `Contacts` resource and then click `Actions` and `Create method`.
- Select `GET` method with `Integration type` as `Lambda`
- Select `Use Lambda Proxy integration`.
- Select the deployment region where the Lambda function will be deployed as `us-east-1`.
- Search for the Lambda function by name such as `serverlessRestApi`.

## Creating a `/contact` endpoint:

- PUT
- GET
- PATCH
- DELETE

# Test API Endpoints in Postman

## GET `/health`
Test the health of the API by sending a GET request to the `/health` endpoint which should return a `200 OK` response.

Request Body:
```json
"None"
```
Response:
```json
"200 OK"
```
## GET `/contacts`
Sending a GET request to the `/contacts` endpoint will return a list of all contacts in the database.
Request Body:
```json
"None"
```
Response:
```json
"200 OK"
```

## POST `/contact`
Add contacts to the database by sending a POST request to the `/contact` endpoint.

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

## GET `/contact?contactId=10004`
Retrieve a single contact using the `/contact` endpoint with `contactId` as q query parameter.

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

## PATCH `/contact`
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

## DELETE `/contact`
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
