![Alt texts](../Images/p1.png)

# Day 110 |  Big Project 1st on CV | CI/CD For Full Stack ChatApp

# Snappy - Chat Application 

![login page](./images/snappy_login.png)

![home page](./images/snappy.png)

## Installation Guide

### Requirements
- [Nodejs](https://nodejs.org/en/download)
- [Mongodb](https://www.mongodb.com/docs/manual/administration/install-community/)

Both should be installed and make sure mongodb is running.
### Installation

#### First Method
```shell
git clone https://github.com/koolkishan/chat-app-react-nodejs
cd chat-app-react-nodejs
```
Now rename env files from .env.example to .env
```shell
cd public
mv .env.example .env
cd ..
cd server
mv .env.example .env
cd ..
```

Now install the dependencies
```shell
cd server
npm install
cd ..
cd public
npm install
```
We are almost done, Now just start the development server.

For Frontend.
```shell
cd public
npm run start
```
For Backend.

Open another terminal in folder, Also make sure mongodb is running in background.
```shell
cd server
npm run start
```

# Part 2 : CI/CD GitHub Action