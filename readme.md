## 1. Project 17 ( Certificate Generator )

### How Works.

Users signup / create account on our site. A template section would be available for each certificates where users could select the type he / she wants. Based on the selected template, users would be taken to a different screen where he/she could fill in necessary data like :-

- COMPANY NAME
- COMPANY LOGO
- TITLE
- SUBTITLE
- REMARKS
- INSTRUCTOR NAME <| optional base on selected template |>
- DIRECTOR NAME <| optional base on selected template |>
- DIRECTOR E-SIGNATURE

![image](https://i0.wp.com/www.templatescatalog.com/wp-content/uploads/2021/12/Professional-Certificate-Template.jpg?fit=860%2C614&ssl=1)

After adding those necessary informaations above, user would be taking to the next phase which is importing `CSV` file. We would let them know what fields are required from the csv, i.e

- RECIEPIENT NAME
- EMAIL ADDRESS.

If those fields above aren't present in the `CSV` file, we simply send an error message to the user. If they are present, we extract the informations present in the csv file ( emails, name ) and store them in our database.

Now based on this informations we got from the `CSV` file, which is also saved in our `database`. we simply iterate over this informations ( id, emails & names) and generate a unique url which contains each users info from the csv. for eg, we simply generate a url in this format.

`https://cv-generator.com/:user_id/:temp_id`. once each url is sent, we leverage [Mail Gun API](https://www.mailgun.com/) for sending each url generated to each email address. This process would be in bulk, so we need to be aware of security levels when sending bulk email. For eg, we do not want other reciepient to see other reciepient email address.

```
 FROM :- cvgenerator@mail.com
 TO :- test1@mail.com,test2@mail.com,test3@mail.com....etc
```

We can solve this issue by using email standard `BCC` instead of `CC`.

>BCC stands for “blind carbon copy.” Just like CC, BCC is a way of sending copies of an email to other people. The difference between the two is that, while you can see a list of recipients when CC is used, that's not the case with BCC.

Once each users get the unique url sent to them, on opening the url (`https://cv-generator.com/:user_id/:temp_id`), we simply extract the query params id from he url, and make a request to our backend API to select information from our table ( email and name and template choose based on the template id ), we would then use use this information to fill in the available certificate template fields. users would simply click on a download button present in that page to download that template as eithe pdf or image.

### Technologies

- Frontend
    - Reactjs
    - Tailwind Css
    - Chakra UI
    - react-html-pdf/png/jpg...

- Backend
  - API
    - Nodejs
    - Typescript
    - Mongodb
 - Automation / Scripting
    - Python
    - FastAPI

## 2. Project 18 ( Weather Forecase App )

Get weather data from a speific location. This project is basically `Frontend Heavy`. The only task here for backend dev is to create a `reverse proxy` as a wrapper for this API, which would be used to store sensitive data along the way, instead of storing this data in client.


### Technologies

- Frontend
    - Reactjs
    - Tailwind Css
    - Chakra UI
    - react-html-pdf/png/jpg...


### [M30 Weather API](https://m3o.com)

#### Usage

```js
POST https://api.m3o.com/v1/weather/Now
Content-Type: application/json
authorization: Bearer <M3O_TOKEN>

{
    "location": "< location_name | IP Address | City Name | Country Name >"
}
```

Response

```json
{
  "location": "Lagos",
  "region": "Lagos",
  "country": "Nigeria",
  "latitude": 6.45,
  "longitude": 3.4,
  "timezone": "Africa/Lagos",
  "local_time": "2022-11-08 8:08",
  "temp_c": 25,
  "temp_f": 77,
  "feels_like_c": 27.3,
  "feels_like_f": 81.1,
  "humidity": 100,
  "cloud": 25,
  "daytime": true,
  "condition": "Mist",
  "icon_url": "//cdn.weatherapi.com/weather/64x64/day/143.png",
  "wind_mph": 2.2,
  "wind_kph": 3.6,
  "wind_direction": "N",
  "wind_degree": 10
}
```