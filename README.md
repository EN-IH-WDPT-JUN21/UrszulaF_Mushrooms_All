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

 <ol>
    <li> discovery-service
    <li> gateway-service
    <li> user-service
    <li> mushroom-service
    <li> event-service
    <li> animal-service      
</ol>

Go to the {{name}}ServiceApplication class in the `src` directory (\src\main\java\com\mushrooms\{{name}}service) and run main method in all of them in above order



### Sample users:

In data.sql files in resources (\src\main\resources) there are some sample data you can already use. For example you can log in with username "Ula" and password "admin" in browser or Postman

You can create your own data the same way.

### API documentation - routes:
These are the routes you can try and the permissions you will need to perform the action:

<ol>
  <li> Admin routes:
      <ul> 
        <li> Accounts: </li>
        <ul>
        <li> Method: GET -- Route: /accounts -- Response: Get all accounts </li>
        <li> Method: GET -- Route: /accounts/{id} -- Response: Get account by account ID </li>
        <li> Method: PATCH -- Route: /accounts/change-balance/{id} -- Response: Update balance amount by account ID </li>
        <li> Method: PATCH -- Route: /accounts/change-status/{id} -- Response: Update status by account ID </li>
        <li> Method: GET -- Route: /checking-accounts -- Response: Get all checking accounts </li>
        <li> Method: POST -- Route: /checking-account/new -- Response: Create a new checking account </li>
        <li> Method: GET -- Route: /credit-card-accounts -- Response: Get all credit cards accounts </li>
        <li> Method: POST -- Route: /credit-card-account/new -- Response: Create a new credit card account </li>   
        <li> Method: GET -- Route: /saving-accounts -- Response: Get all saving accounts </li>
        <li> Method: POST -- Route: /saving-account/new -- Response: Create a new saving account </li>   
        <li> Method: GET -- Route: /student-checking-accounts -- Response: Get all student checking accounts </li>
        <li> Method: POST -- Route: /student-checking-account/new -- Response: Create a new student checking account </li>   
        <li> Method: GET -- Route: /transactions -- Response: Get all transactions (internal) </li>
        <li> Method: GET -- Route: /third-party-send-transactions -- Response: Get all third party send transactions </li>
        <li> Method: GET -- Route: /third-party-receive-transactions -- Response: Get all third party send transactions </li>
        </ul>        
        <li> Account Holders: </li>
        <ul>        
            <li> Method: GET -- Route: /account-holders -- Response: Get all Account Holders </li>
            <li> Method: GET -- Route: /account-holders/{id} -- Response: Get Account Holder by Account Holder ID </li>
            <li> Method: POST -- Route: /account-holders/new -- Response: Create a new Account Holder </li>
        </ul>        
        <li> Third Parties: </li>
        <ul>        
        <li> Method: GET -- Route: /third-parties -- Response: Get all Third Parties </li>
        <li> Method: POST -- Route: /third-parties/new -- Response: Create a new Third Party </li>    
        </ul>        
      </ul>    
  </li>
    <li> User routes:
      <ul> 
        <li> Method: GET -- Route: /my-accounts/primary/ -- Response: Get all primary accounts of a user by Account Holder ID </li>
        <li> Method: GET -- Route: /my-accounts/secondary -- Response: Get all secondary accounts of a user by Account Holder ID </li>
        <li> Method: GET -- Route: /my-accounts/{id}/balance -- Response: Get balance by account ID </li>
        <li> Method: POST -- Route: /transfer -- Response: Make a transaction between accounts </li> 
        <li> Method: POST -- Route: /third-party/send-money/{hashed-key} -- Response: Send money from accounts to Third Party by Hashed key</li> 
      </ul>    
  </li>

</ol>

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
