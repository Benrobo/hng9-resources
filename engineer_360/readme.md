# 360deg Skill Evaluator

## Project Description

Engineering Team 360° skill evaluator. This is for companies that want to know how good their engineers are. Engineers register and get various multi-choice questions on different topics. The tool builds a profile of each engineer in the form of a spiderweb chart, so the company knows where engineers need to improve.


## Backend Technologies

### API Development.    
    1. PHP / LARAVEL

    2. Reddis ( in-memory caching ).

### Database Management
    1. MYSQL


# System Architecture

![image](https://github.com/Benrobo/hng9-resources/blob/main/images/architecture.png?raw=true)

# App Flow Architecture

![image](https://github.com/Benrobo/hng9-resources/blob/main/images/app_flow.png?raw=true)

# Database Schema Design

![image](https://github.com/Benrobo/hng9-resources/blob/main/images/db_design.png?raw=true)

# Sequence Diagram

![image](https://github.com/Benrobo/hng9-resources/blob/main/images/sequence.jpg?raw=true)


# API ROUTE'S DESIGN

## Create an Account

> REQUEST
```js
curl --location --request POST '/api/v1/auth/register' \
--data-raw '{
	"first_name": "Dev",
	"last_name": "Bash",
	"username": "bash",
	"type": "user",
	"email": "bash32@gmail.com",
	"password": "bash"
}'
```

> RESPONSE

```js
{
  "error": false,
  "message": "Acount created successfully",
  "code": 200,
  "data": {
    "id": "6edewd2e32s-e32dexwqd2e32d-d223",
    "first_name": "Dev",
    "last_name": "Bash",
    "username": "bash",
    "type": "user",
    "email": "bash32@gmail.com"
  }
}
```

## Add Employee

> REQUEST
```js
curl --location --request POST '/api/v1/employee/add' \
--header 'Authorization: Bearer <JWT_TOKEN>' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Brain John",
    "email": "brain@testmail.com",
    "occupation": "Software Engineer",
    "phonenumber": "1234567890"
}'
```

> RESPONSE

```js
{
  "error": false,
  "message": "Employee added successfully",
  "code": 200,
  "data": {
    "name": "Brain John",
    "email": "brain@testmail.com",
    "occupation": "Software Engineer",
    "phonenumber": "1234567890"
  }
}
```

## Get Assessments

> REQUEST
```js
curl --location --request GET '/api/v1/assessments/get' \
--header 'Authorization: Bearer <JWT_TOKEN>' \
--header 'Content-Type: application/javascript' \
```

> RESPONSE

```js
{
  "error": false,
  "message": "Assessments fetched successfully",
  "code": 200,
  "data": [
    {
      "name": "Software Engineering",
      "expiry": "16996534345",
      "status": "opened",
      "created_at": "64534524342"
    }
  ]
}
```
