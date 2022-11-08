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

## 2. Project 18 ( Rain When )

A weather app for Nigeria. It does not tell you about temparature or other unneccessary info. It just tells you in a simple format if it will rain today or not, and what time it will start raining. So you know if to take umbrella

Get weather data from a speific location. This project is basically `Frontend Heavy`. The only task here for backend dev is to create a `reverse proxy` as a wrapper for this API, which would be used to store sensitive data along the way, instead of storing this data in client.

![image](https://cdn.dribbble.com/users/6400757/screenshots/16952894/media/5e1f109e23589152c1ff8098d96dd802.png)

![image](https://cdn.dribbble.com/users/6259454/screenshots/17003404/media/6695237e281547ae9af43629d7849490.png)

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

From the response gotten, we should be able to tell if it would rain or not.

## 3. Project 19 ( Real Exchange Rate ) .
Is it 410 per dollar or is it 820? How about in Columbia? An app that tells you real "street" exchange rate for every country.

![image](https://cdn.dribbble.com/users/758684/screenshots/17714477/media/24121cdcaf0e18dddff751ee9812229e.jpg)

![image](https://cdn.dribbble.com/userupload/3589607/file/original-701d39ad405f561a0fa73df66df85838.png)

### Idea.
We need to make this app look interactive and engaging. we could come up with an app that has an in-built google map, where users could search a country name with autocomplete feature.After completing the country name, we simply animate the google map to point to that address / country name. 

Then at the bottom of the app, we display the exchange rate of that country name using the country code i.e ( `USD`, `NGN`, `CAD` ). we then this information, make a request to our api to provide us with current exchange rate based on the country code given. for example.

```js
GET https://www.freeforexapi.com/api/live?pairs=USDNGN

Content-Type: application/json
```

Response
```json
{
  "rates": {
    "USDNGN": {
      "rate": 439.759976,
      "timestamp": 1667897103
    }
  },
  "code": 200
}
```

This api works differently. what you need to do, is specify the `To` and `From` country code.
```js

// TO=NGN
// FROM=USD
https://www.freeforexapi.com/api/live?pairs={TO}{FROM}
```