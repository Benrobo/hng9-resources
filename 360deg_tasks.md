# App Flow

# Authentication / Authorization.

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
<br />

> Note!! both `company` and `staff` `profiles` are visible in `public`, but some `UI components` would differentiate them.

## Company `Admin` Dashboard

As stated earlier, the company admin dashboard defers from the regular staffs dashboard. Below are some of the pages only `visible` to the `admin`. 

### Pages ( `Only` Visible to `Admin` )

1. Space Section :- This is a section where the admin of the company would create different space based on the occupations of some employers.. for eg, spaces could be `Petroleum`, `Automotive Engineering`, `Wood Worker`, `Software Engineering`. Each space created, has a section within the space where the admin could add different questions related to the space.. i.e `Petroleum` space would contain `Petroleum` base questions, and `Software Engineering` space, would contain software engineering questions.


2. Add Staff's :- This is a section where the admin could add other members of staff using `2` different methods..

    a. Add company staff members to the system using a `form` components that contains the following fields ( `Email`, `Question_Category`, `Full Name`, `Username` ).
    b. A section where admin could upload a `CSV` file having the following fields ( `Email`, `Question_Category`, `Full Name`, `Username` ). along with all staff data / info.

Doing this simply does two things. ( 1 ). Stores the user info in database.  ( 2 ) generate a unqiue `URL` which is been sent to all staffs email address. The url could be something like this `https://axle.multiplex.com/evaluate/org_id/exp_id`. The `exp_id` is used to track if that link sent has expired or not. If the link has been expired, a Not found page shows up.

If an unauthenticated staff opens this link, a signin form would be displayed for them to signin, else, they would be redirected to the assessment page.

3. All Staff's :- This is a section where the admin could `manage` all registered staff within the system.. from `updating` users `permission` level to `deleting` / `removing` a specific user from the system.

4. Questions / Answers Tab :- This is a section where the admin of the system is able to add company personal questions instead of depending on some existing `API` which produces random questions. Question and Answers could be added in different categories.. A `UI` component would have the following fields present.

    a. Question Description. :- `Actual Question`
    b. multiple_choice :- `true` or `false`
    c. Select Space :- responsible for setting the category of the question been added.
    d. Answers :- if `multiple_choice` is selected, admin would be able to add multiple answers and select which answers are meant to be correct or not.

5. Assessment Section :- This is a section where the admin or anyone who has an `Admin` priveledge, would be able to see all `Users` and also view their score so far based on each assessment. Bonus feature :- the admin / company could deside to reward this user some badge as seen in the picture below if he/she did well during the task.
6. 
### Pages ( Visible to `Both` `Admin` and `User` )

1. Settings Page :- This is a page where each user could manage their data, from `Updating Password` to `Updating Personal Info` .i.e `Email`, `Username`, `Image`, `Full Name`, `Delete Account`, `Logout`, ( for admin only (`Add Company subdomain slug/name`) )..etc

2. Profile Page :- This is a section meant to manage the user profile. Users has the right to set their profile to be `Public` or `Private`.. If the logged in user is a staff, there would be a section where all `Passed` and `Failed` Questions would be. Also, a `Spider Chart` would be presented to show other companies how well a user did.
3. 
> Some useful update...

Admin of the system has the feature to add employees to a specific space.. if they want some certain numbers of employees to be in a specific space , this can be done also..


## App Architecture

![image](https://github.com/Benrobo/hng9-resources/blob/main/architecture.png?raw=true)

## App Workflow

![image](https://github.com/Benrobo/hng9-resources/blob/main/architect.png?raw=true)

## Database Design Schema 
> Still under development

Database Architecture was constructed using the link [Database Architecture](https://dbdiagram.io/d/636cce5fc9abfc611171a876)

![image](https://github.com/Benrobo/hng9-resources/blob/main/db_design.png?raw=true)



... More Info would be added later on, Keep an eye on this file.
