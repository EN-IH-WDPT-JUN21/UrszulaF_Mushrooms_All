# Mushrooms Webpage 


Final project about Mushrooms by Urszula Figurska

Back-end: https://github.com/UrszulaF/UrszulaF_Mushrooms_Backend.git

Front-end: https://github.com/UrszulaF/UrszulaF_Mushrooms_Frontend.git

## Intro
This is Webpage for mushroom-picking fans. There is information about main mushrooms in Poland, rules and advices for mushroom pickers, events & some animals information.

It allows to:
<ul>
  <li> Join as a user after registering </li>
  <li> Login/logout to the page </li>
  <li> Update user details </li>
  <li> Find out more about mushrooms in Polish forests </li>
  <li> Get some piece of rules and advices for mushroom fans </li>
   <li> Read about some animals that can be encountered in forests in Poland </li>
  <li> More functionalities for Admins: get, create, update & delete part of information about users, mushrooms, events </li>
</ul>

## Back-end


### Prerequisites

This a list of minimum requirements to run the program:

* [Java SE 17](https://www.oracle.com/java/technologies/javase-downloads.html)

### Installation


Clone/download the repo from this site:
   ```sh
   git clone https://github.com/UrszulaF/UrszulaF_Mushrooms_Backend.git
   ```
To run this project locally do the following after cloning or downloading the project:

<ol>
  <li> Open the project on your IDE such as IntelliJ </li>
  <li> Create the databases in MySQL: mushroomapp. 
    Just run "create database mushroomapp;" and then "use mushroomapp;". </li>
  <li> Edit the application.properties file in the main folder in all services and insert your own credentials.
  Alternatively give credential to username ironhacker and password 1r0nH@ck3r in MySQL:
   
   ```sh
CREATE USER 'ironhacker'@'localhost' IDENTIFIED BY '1r0nH@ck3r';

GRANT ALL PRIVILEGES ON *.* TO 'ironhacker'@'localhost';

FLUSH PRIVILEGES;
   ```
    
</ol>


### Structure

There are 6 services: 


| Port | Service
| :--- | :--- 
| 8761 | discovery-service
| 8000 | gateway-service
| 8100 | mushroom-service
| 8200 | event-service
| 8300 | user-service
| 8400 | animal-service     


Go to the {{name}}ServiceApplication class in the `src` directory (\src\main\java\com\mushrooms\{{name}}service) and run main method in all of them in above order



### Sample users:

In data.sql files in resources (\src\main\resources) there are some sample data you can already use. For example you can log in with username "Ula" and password "admin" in browser or Postman

You can create your own data the same way.

### API documentation - routes:
These are the routes you can try and the permissions you will need to perform the action:

#### gateway-service (http://localhost:8000)
Some of the routes require running user-service!

| Endpoint | Method | Description | Path Params | Body| Token*
| :--- | :--- | :--- | :---  | :--- | :--- 
| /token| `POST` | Generate JWT token | None | Yes** | No
| /api/users-auth | `GET` | Get all users-auth DB info | None | None | Yes
| /api/users-auth/all | `GET` | Get all users-auth + user DB info | None | None  | Yes
| /api/users-auth/{username} | `GET` | Get users-auth + user DB info by username | `username=[String]` | None  | Yes
| /api/users-auth/name/{username} | `GET` | Get usersname from DB | `username=[String]` | None  | No
| /api/users-auth/new | `POST` | Add new user | None | Yes***   | Yes
| /api/users-auth/update/{username} | `PUT` | Update user info | `username=[String]`| Yes****  | Yes
| /api/users-auth/delete/{username} | `DELETE` | Delete user info| `username=[String]`| None  | Yes


*requires token - first generate token by POST /token method and then use in Postman as new Header Authorization + Bearer {{token}}

**POST /token - example body:

    {
    "username": "Ula",
    "password": "admin"
    }



***POST /api/users-auth/new - example body:


    {
    "username": "Felix",
    "email": "f@f.pl",
    "password": "admin",
    "role": "ADMIN",
    "photoURL": "some photo",
    "bio": "I'm user"
    }

****PUT /api/users-auth/update/{username} - example body:

    {
    "email": "felix@f.pl",
        "bio": "I'm great"
    }

#### mushroom-service (http://localhost:8100)


| Endpoint | Method | Description | Path Params | Body| Token*
| :--- | :--- | :--- | :---  | :--- | :--- 
| /api/mushrooms | `GET` | Get all mushrooms | None | None | No
| /api/mushrooms/{mushroomName} | `GET` | Get mushrooms by mushroomName | `mushroomName=[String]` | None  | No
| /api/mushrooms/id/{id} | `GET` | Get mushrooms by id | `id=[long]` | None  | No
| /api/mushrooms/containing/{mushroomName} | `GET` | Get mushrooms by the part of mushroomName | `mushroomName=[String]` | None  | No
| /api/mushrooms/new | `POST` | Add new mushroom | None | Yes**   | No
| /api/mushrooms/update/{id} | `PUT` | Update mushroom info | `id=[long]`| Yes***  | No
| /api/mushrooms/delete/{id} | `DELETE` | Delete mushroom info| `id=[long]`| None  | No


*requires token - first generate token by POST /token method and then use in Postman as new Header Authorization + Bearer {{token}}

**POST /api/mushrooms/new - example body:

    {
    "photoURL": "",
    "mushroomName": "test",
    "otherNames": "test",
    "edible": true,
    "consumable": "GREAT",
    "whenFruiting": "summer-autumn",
    "whereFruiting": "deciduous and coniferous forests, especially in mountains",
    "hat": "3-10cm, yellow, at first convex, later concave, surface irregular, undulating, folded edge",
    "stem": "massive, smooth, in the shape of an inverted cup",
    "ring": "none",
    "gills": "yellow, folded, twisted, bifurcated and running far away",
    "tubes": "none",
    "pulp": "yellowish, compact and fibrous",
    "smell": "fruity",
    "taste": "sweet to spicy",
    "differentiation": "color from pale yellow to golden yellow, sometimes orange",
    "similar": "false chanterelle",
    "remarks": "",
    "foodValue": "edible, delicious, it can be prepared in many ways"
    }


***PUT /api/mushrooms/update/{id} - example body:

    {
    "mushroomName": "change",
    "otherNames": "change",
    "edible": false
    }

#### event-service (http://localhost:8200)


| Endpoint | Method | Description | Path Params | Body| Token*
| :--- | :--- | :--- | :---  | :--- | :--- 
| /api/events | `GET` | Get all events | None | None | No
| /api/events/{eventName} | `GET` | Get events by eventName | `eventName=[String]` | None  | No
| /api/events/id/{id} | `GET` | Get mushrooms by id | `id=[long]` | None  | No
| /api/events/type/{eventType} | `GET` | Get events by eventType | `eventType=[String]` | None  | No
| /api/events/new | `POST` | Add new event | None | Yes**   | No
| /api/events/update/{id} | `PUT` | Update event info | `id=[long]`| Yes***  | No
| /api/events/delete/{id} | `DELETE` | Delete event info| `id=[long]`| None  | No


*requires token - first generate token by POST /token method and then use in Postman as new Header Authorization + Bearer {{token}}

**POST /api/events/new - example body:

    {
    "eventName": "grzybobranie",
    "eventType": "MUSHROOM_PICKING",
    "whenEvent": "2022-07-01T09:00:00",
    "duration": 500,
    "whereEvent": "forest in Stara Milosna",
    "contactPerson": "Ewa",
    "description": "I invite you for June mushroom picking. Let me know if you want to come"
    }


***PUT /api/events/update/{id} - example body:

    {
    "whenEvent": "2022-08-01T09:00:00",
    "duration": 500,
    "whereEvent": "forest in Stara Radosna",
    "contactPerson": "Ewa",
    "description": "Postpone"
    }

#### user-service (http://localhost:8300)


| Endpoint | Method | Description | Path Params | Body| Token*
| :--- | :--- | :--- | :---  | :--- | :--- 
| /api/users | `GET` | Get all users | None | None | No
| /api/users/{username} | `GET` | Get users by username | `username=[String]` | None  | No
| /api/users/id/{id} | `GET` | Get users by id | `id=[long]` | None  | No
| /api/users/new | `POST` | Add new user | None | Yes**   | No
| /api/users/update/{username} | `PUT` | Update user info | `username=[String]`| Yes***  | No
| /api/users/delete/{username} | `DELETE` | Delete user info| `username=[String]`| None  | No


*requires token - first generate token by POST /token method and then use in Postman as new Header Authorization + Bearer {{token}}

**POST /api/users/new - example body:

    {
    "id": 7,
    "photoURL": "sth",
    "username": "Felix",
    "bio": "I'm user"
    }


***PUT /api/users/update/{username} - example body:

    {
    "photoURL": "",
    "bio": "I'm great"
    }

#### animal-service (http://localhost:8400)


| Endpoint | Method | Description | Path Params | Body| Token*
| :--- | :--- | :--- | :---  | :--- | :--- 
| /api/animals | `GET` | Get all animals | None | None | No
| /api/animals/{animalName} | `GET` | Get animals by animalName | `animalName=[String]` | None  | No
| /api/animals/id/{id} | `GET` | Get animals by id | `id=[long]` | None  | No
| /api/animals/containing/{animalName} | `GET` | Get animals by the part of animalName | `animalName=[String]` | None  | No
| /api/animals/new | `POST` | Add new animal | None | Yes**   | No
| /api/animals/update/{id} | `PUT` | Update animal info | `id=[long]`| Yes***  | No
| /api/animals/delete/{id} | `DELETE` | Delete animal info| `id=[long]`| None  | No


*requires token - first generate token by POST /token method and then use in Postman as new Header Authorization + Bearer {{token}}

**POST /api/animals/new - example body:

    {
    "photoURL": "",
    "animalName": "zwierzak",
    "otherNames": "zwierz",
    "animalType": "arachnid",
    "animalSize": "12cm",
    "description": "descr",
    "remarks": "remark"
    }


***PUT /api/animals/update/{id} - example body:

    {
    "photoURL": "photo",
    "animalName": "super zwierzak"
    }

## Database diagram:
![diagram](https://user-images.githubusercontent.com/85784274/146441011-9206a45d-7021-4a21-99a4-2b1b723fb698.png)


Each service have separate database. In gateway service there is security information about users in user_auth and it's protected by JWT token. If you want to see this information you have to login in Mushroom page as a user write Autorization "Bearer {token}" in Postman 

## Front-end
Link: https://github.com/UrszulaF/UrszulaF_Mushrooms_Frontend.git

### Prerequisites

This a list of minimum requirements to run the program:


* [Visual Studio Code](https://code.visualstudio.com/)

* [Angular CLI](https://github.com/angular/angular-cli) version 12.2.10.



### Installation

Clone/download the repo from this site:

To run this project locally do the following after cloning or downloading the project:

<ol>
  <li> Open the project on Visual Studio Code </li>
  <li> in terminal run:  npm i  </li>
  <li> in terminal run: ng serve </li>  
   <li> Open http://localhost:4200/ </li>  
</ol>

### Guide

<ol>
  <li> Home page </li>
  <ol>
    <li> After opening in your browser, Home page will be shown. Here you can read basic guidlines for mushroom pickers. </li>
    <li> When you decide what you want to do next select one of the buttons or pick option from Menu </li>
    <li> You can change language from English to Polish (Menu ->Select Language). Translation still in progress. </li>
  </ol>
  <li> Register page </li>
  <ol>  
    <li> In order to see some information you have to register and login. </li>
    <li> There are 3 types of Role: Standard user, Premium user (creative role: adds, update data) or Admin (administrator) </li>
    <li> You can't register as Admin. This role is given on back-end side </li>
  </ol>  
  <li> Login page </li>
  <ol> 
    <li> After successful registration, you can log in. </li>
    <li> If you don't want to register you can use sample data for example you can log in with username "Ula" and password "admin" in browser. </li>
    <li> To see full capabilities log in as one of the users with Admin role (for example username "Ula" and password "admin"). </li>
  </ol>
  <li> User profile </li>
  <ol> 
    <li> After passing right credentials you will be redirected to User profile page. Here you can read your data, update some or all of them </li> 
  </ol>
  <li> Mushrooms</li>
  <ol> 
    <li> Here you can read about mushrooms that are mostly picked in Poland </li> 
    <li> You can search by a part of name</li> 
    <li> When you click inside the table it will show detailed information about selected mushroom </li> 
    <li> (PREMIUM/ADMIN) Add mushroom button will take you to the form</li> 
  </ol>
  <li> New Mushroom </li>
  <ol>
     <li> Here you can add new mushroom to our database. Please send us photo via email.</li> 
  </ol> 
  <li> Mushroom details </li>
  <ol>
     <li> Here you can read more about selected mushroom and see some photos</li> 
      <li> (PREMIUM/ADMIN) Update button will take you to the form to update data</li> 
      <li> (ADMIN) Delete button will delete information, but you will be asked to confirm</li> 
  </ol> 
  <li> Mushroom update </li>
  <ol>
      <li> (PREMIUM/ADMIN) Here you can update data. Please send us photo via email if you want to change it. </li> 
  </ol> 
  <li> Events</li>
  <ol> 
    <li> Here you can read about events that our members organize </li> 
    <li> You can search by a type of event</li> 
    <li> When you click inside the table it will show detailed information about selected event </li> 
    <li> (PREMIUM/ADMIN) Add new event button will take you to the form</li> 
  </ol>
  <li> New Event </li>
  <ol>
     <li> Here you can add new event to our database.</li> 
  </ol> 
  <li> Event details </li>
  <ol>
     <li> Here you can read more about selected event</li> 
      <li> (PREMIUM/ADMIN) Update button will take you to the form to update data</li> 
      <li> (ADMIN) Delete button will delete information, but you will be asked to confirm</li> 
  </ol> 
  <li> Event update </li>
  <ol>
      <li> (PREMIUM/ADMIN) Here you can update data. </li> 
  </ol>  
    <li> Quiz </li>
  <ol>
      <li> Here you can check your knowledge if you know the mushrooms from our database. There is one important question "Is it edible? True or False" </li> 
      <li> Select option and press check. You will see the answer immediately </li>
       <li> Click next to see next question </li>
       <li> At the end you will see your score and which answers you have right. </li>
       <li> You can try again or go to Mushrooms page to improve your knowledge </li>
  </ol>  
    <li> Animals</li>
  <ol> 
    <li> Here you can read about animals mushroom picker can most often encounter in forests in Poland </li> 
    <li> You can search by a part of name</li> 
    <li> When you click inside the table it will show detailed information about selected animal </li> 
    <li> (PREMIUM/ADMIN) Add animal button will take you to the form</li> 
  </ol>
  <li> New Animal </li>
  <ol>
     <li> Here you can add new animal to our database. Please send us photo via email.</li> 
  </ol> 
  <li> Animal details </li>
  <ol>
     <li> Here you can read more about selected animal and see some photos</li> 
      <li> (PREMIUM/ADMIN) Update button will take you to the form to update data</li> 
      <li> (ADMIN) Delete button will delete information, but you will be asked to confirm</li> 
  </ol> 
  <li> Animal update </li>
  <ol>
      <li> (PREMIUM/ADMIN) Here you can update data. Please send us photo via email if you want to change it. </li> 
  </ol> 
      <li> (ADMIN) User list</li>
  <ol> 
    <li> (ADMIN) Here Admins can read about members </li> 
    <li> (ADMIN) You can search by a part of name</li> 
      <li> (ADMIN)  Update button will take you to the form to update data</li> 
      <li> (ADMIN) Delete button will delete information, but you will be asked to confirm</li> 
  </ol> 
    <li> Contact us </li>
  <ol>
      <li> Here you can read how to contact us </li> 
  </ol> 
</ol>


Thank you,

Urszula Figurska
