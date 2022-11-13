# 360deg Skill Evaluator

## Project Description

Engineering Team 360° skill evaluator. This is for companies that want to know how good their engineers are. Engineers register and get various multi-choice questions on different topics. The tool builds a profile of each engineer in the form of a spiderweb chart, so the company knows where engineers need to improve.


# App Features

- Authentication / Authorization.
- Adding of employees.
- Creating of Assessments of various categories.
- Creating of Assessmentsestions.
- Assigning employees to a specific assessments.
- Visualization of assessments scores using `Spider Web Chart`.



## Authentication / Authorization.

User should be able to perform every sort of authentication (`Login` / `Signup`). On registering, each user who signedup for an organization, would be given a unique dashboard from regular staff. But before this process, the user would get a `Email` verification code. This process is to prevent other malicious users from registering in behalf of the user credentials.

## Signup Info Needed..

- Email ( user email address ).
- Username.
- Company Name.
- Company Email
- Password.
- Confirm Password.

## Login Info Needed

- Email
- Password
- Forget Pasword / Reset Password

## Resetting Password..
During this process, a different page would be available and a form for the user to pass in their email address fo password resetting.

Once user authentication is successfull enough, we simply redirect them to dashboard. Company staff (`admin`) dashboard defer from the normal company organization staffs.

Below are the `pages` and `component` needed to be shown on companies `admin` dashbobard and normal `staff` dashboard.

During creation of every accounts, each user is assigned a temporary `profile image` using this libary called [Avatar Dicebear](https://avatars.dicebear.com/).. a preview of a nice looking avatar image can be seen below :-
<br />
<p>
<img src="https://avatars.dicebear.com/api/micah/mark.svg" width="80">
<img src="https://avatars.dicebear.com/api/identicon/mark.svg" width="80">
<img src="https://avatars.dicebear.com/api/initials/mark.svg" width="80">
</p>
<br />

> Note!! both `company` and `staff` `profiles` are visible in `public`, but some `UI components` would differentiate them.

## Company `Admin` Dashboard

As stated earlier, the company admin dashboard defers from the regular staffs dashboard. Below are some of the pages only `visible` to the `admin`. 

### Pages ( `Only` Visible to `Admin` )

1. Assessments Section :- This is a section where the admin of the company would create different assessment based on the occupations of some employers.. for eg, assessments could be `Petroleum`, `Automotive Engineering`, `Wood Worker`, `Software Engineering`. Each assessment created, has a section where the admin could add different questions related to the assessment category.. i.e `Petroleum` assessment would contain `Petroleum` base questions, and `Software Engineering` assessment, would contain software engineering questions.


2. Add Staff's :- This is a section where the admin could add other members of staff using `2` different methods..

    a. Add company staff members to the system using a `form` components that contains the following fields ( `Email`, `Full Name`, `Username` ).
    b. A section where admin could upload a `CSV` file having the following fields ( `Email`, `Full Name`, `Username` ). along with all staff data / info.

Doing this simply does two things :
1. Stores the user info in database.  
2. generate a unqiue `URL` which is been sent to all staffs email address. The url could be something like this `https://axle.multiplex.com/evaluate/org_id/exp_id`. The `exp_id` is used to track if that link sent has expired or not. If the link has been expired, a Not found page shows up.

If an unauthenticated staff opens this link, a signin form would be displayed for them to signin, else, they would be redirected to the assessment page.

3. All Staff's :- This is a section where the admin could `manage` all registered staff within the system.. from `updating` users `permission` level to `deleting` / `removing` a specific user from the system.

4. Questions / Answers Tab :- This is a section where the admin of the system is able to add company personal questions instead of depending on some existing `API` which produces random questions. Question and Answers could be added in different categories.. A `UI` component would have the following fields present.

    a. Question Description. :- `Actual Question`
    b. multiple_choice :- `true` or `false`
    c. Select Space :- responsible for setting the category of the question been added.
    d. Answers :- if `multiple_choice` is selected, admin would be able to add multiple answers and select which answers are meant to be correct or not.

5. Statistics Section :- This is a section where the admin or anyone who has an `Admin` priveledge, would be able to see all `Users` and also view their score so far based on each assessment in form of a `Spider Web Chart` or a `Radar Chart`

## Backend Technologies

### API Development.    
1. `PHP / LARAVEL` :- `Laravel` is a web application framework with `expressive`, `elegant` syntax.freeing you to create without sweating the small things.

2. `Reddis` ( in-memory caching ). :- Redis' an in-memory data store with speed making it ideal for `caching` database `queries`, complex `computations`, `API` calls, and `session` state.

### Database Management
1. `MYSQL` :- Relational Database Management System


# System Architecture
This diagram depict the system architecture from a development perspective.

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
```sh
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

```json
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
```sh
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

```json
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
```sh
curl --location --request GET '/api/v1/assessments/get' \
--header 'Authorization: Bearer <JWT_TOKEN>' \
--header 'Content-Type: application/javascript' \
```

> RESPONSE

```json
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