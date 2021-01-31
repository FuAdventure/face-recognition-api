# Face Recognition Web Development (Back end)
This repository contains the back end code for this project. The front end code can be found [here](https://github.com/FuAdventure/face-recognition-web-app)

A version deployed on Heroku can be tried out [here](https://face-recognition-vd.herokuapp.com/). To  use the face recognition web, register or sign in, then simply paste a image url, [like this](https://goop-img.com/wp-content/uploads/2020/06/Mask-Group-2.png), to see the image displayed with the face in it marked by a square frame.

The back end was built with Node.js and Express.js. It works with the front end and a PostgreSQL database (connected to the back end with knex.js). When a user register at the front end, the back end will store the user info in the database (name, email, joined time, hashed password, entry count). When a user tries to sign in, the back end will fecth the submitted info and compared it with that in the database, the user can log in if they match. Passwords were hashed by bcrypt.js. When user enter a image url, the backend will uptate the count of the user's entry in the database and send it to the front end to display. To protect our Clarifai key, requests to Clarify API were sent from the back end and responses will be send to the front end to display face recognition results.

#### Tips to adapt it for your own use:
1. Clone this repo
2. Run `npm install`
3. Run `npm start`
4. You must add your own API key in the `controllers/image.js` file to connect to Clarifai API. You can grab Clarifai API key [here](https://www.clarifai.com/)
5. Add your own database credentials to `server.js` line 12. Besides the back end code, the app also requires a PostgreSQL database which can be created and linked to your app easily on Heroku, remember to change the connection to the right dababase.
6. Our database contains two tables to store the user and login info, created by queries below:
<br>CREATE TABLE users( 
<br>	id serial PRIMARY KEY, 
<br>	name VARCHAR(100),
<br>	email text UNIQUE NOT NULL,
<br>	entries BIGINT DEFAULT 0,
<br>	joined TIMESTAMP NOT NULL
<br>);
<br>CREATE TABLE login(
<br>	id serial PRIMARY KEY,
<br>	hash varchar(100) NOT NULL,
<br>	email text UNIQUE NOT NULL
<br>);
<br>7. In line 34 of "server.js", for deployment, you need to make sure the port that the app listens to is the one it gets from the deployment platform instead of the local port 3000. In our case, we use process.env.PORT.
