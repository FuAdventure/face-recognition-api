# Face Recognition Web Development (Back end)
This repository contains the back end code for this project. The front end code can be found [here](https://github.com/FuAdventure/face-recognition-web-app)

A version deployed on Heroku can be tried out [here](https://face-recognition-vd.herokuapp.com/). To  use the face recognition web, register or sign in, then simply paste a image url, [like this](https://goop-img.com/wp-content/uploads/2020/06/Mask-Group-2.png), to see the image displayed with the face in it marked by a square frame.

1. Clone this repo
2. Run `npm install`
3. Run `npm start`
4. You must add your own API key in the `controllers/image.js` file to connect to Clarifai API. You can grab Clarifai API key [here](https://www.clarifai.com/)
5. Add your own database credentials to `server.js` line 12. Besides the back end code, the app also requires a PostgreSQL database which can be created and linked to your app easily on Heroku, remember to change the connection to the right host.
6. Our database contains two tables to store the user and login info, created by queries below:
CREATE TABLE users(
	id serial PRIMARY KEY, 
	name VARCHAR(100),
	email text UNIQUE NOT NULL,
	entries BIGINT DEFAULT 0,
	joined TIMESTAMP NOT NULL
);

CREATE TABLE login(
	id serial PRIMARY KEY,
	hash varchar(100) NOT NULL,
	email text UNIQUE NOT NULL
);
7. In line 34 of "server.js", for deployment, you need to make sure the port that the app listens to is the one it gets from the deployment platform instead of the local port 3000. In our case, we use process.env.PORT.
