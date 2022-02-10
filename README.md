# MVC, Mongoose

Use this repository for understanding:

- MVC simplified
- Create a server using express-generator
- Folder/file structure for Model, View, Controller
- Packages used
- Connecting MongoDB to Node Express server

## What is MVC?

MVC is an acronym for Model-View-Controller.

### Model

Data: Manages the data and defines the data structure

### View

User Interface: What people see on the browser, displays the data requested

### Controller

Logic: controls the logic that connects the View and the Model. It takes user input, such as clicking or typing, and handles the response for user interactions.

## express-generator

creates a skeleton of an express application.

1. Create a Github repository with readme and .gitignore for Node
2. Clone repo down, run in terminal `npx express-generator --view=ejs "Github repo name"`
3. Cd inside Github repo name, npm i
4. In terminal `code .` to open the express application

## Understanding some of of the folders/files

### bin/www

This folder/file creates a http server by grabbing app.js and sets a port to 3000 (or any port you wish to change to) if there's not PORT in the .env file.
It separates the startup configuration from app.js (Less code in app.js)
That's why in `package.json` script, it has `node ./bin/www`

### node_modules

Holds all dependencies for you project.
Always add /node_modules inside .gitignore, do not want to push up all these files up to Github.
Do not touch

### public

Holds all the static files, such as images, and css

### routes

Where we will mainly work off of.
Will hold all the routers file and folders for different routes

### routes/user

Holds all user related model and controller

### routes/recipe

Holds all recipe related model and controller

### views (Won't be used once we begin to use React for view)

Holds template files for what users see.

## Packages needed:

### dotenv, .env

This npm package helps load environment variables from the .env file. The .env file is a hidden file used to store environment variables, such as PORT or MONGODB_URI. This file is usually not uploaded to Github, so .env should be inside the .gitignore along with /node_modules.

1. In terminal `npm i dotenv`
2. In app.js:
   a. Below var logger = require("morgan") type `require("dotenv").config()` to use the dotenv package
3. You can now access all variables inside the .env file by using process.env.VARIABLE_NAME
4. Create a .env file in the root folder.
5. You can now put your PORT and other important variables inside. Useful for 3rd party API keys.
6. All variables are in capital letters.

### mongoose

Mongoose is a Object Data Modeling (ODM) library for MongoDB and Node.js. We use it to define the schema for our data and creates a model where we can communicate with mongodb regarding our data.

1. In order to use mongodb with our express application, we need to connect them through mongoose
2. In terminal `npm i mongoose`
3. In app.js:
   a. Before our dotenv require, require mongoose: `const mongoose = require("mongoose")`
   b. After our dotenv require:
   ```
   mongoose
   .connect(process.env.MONGODB_URI)
   .then(() => {
    console.log("connected to mongodb");
   })
   .catch((error) => {
    console.log(error);
   });
   ```
4. mongod uri defines the connection:
   MONGODB_URI = mongodb://localhost:27017/[name of database]
   -mongodb:// is required in a standard connection
   -localhost:27017 is mongodb's default port when mongobd is running -[name of database] where you will find all the collection of data saved. Use different name for every application
