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
![diagram](https://user-images.githubusercontent.com/85784274/145723321-a48defdf-4976-4256-8e34-cda0457e4ff0.png)

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

In order to see some information you have to register and login. If you don't wanto to register you can use sample data for example you can log in with username "Ula" and password "admin" in browser.

Thank you,

Urszula Figurska
