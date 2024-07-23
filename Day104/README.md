![Alt texts](../Images/p1.png)
# Day 104 | Use EC2 Ubuntu setup Full stack NextJS + NestJS + Database
### Install Node v20
Link: https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-22-04 
```sh
node -v
npm -v
```
### Setup NextJS
Link: https://www.digitalocean.com/community/developer-center/deploying-a-next-js-application-on-a-digitalocean-droplet
```sh
npx create-next-app my-next-app
cd my-next-app

npm start

```
### Setup NestJS
Link: https://www.digitalocean.com/community/tutorials/how-to-deploy-a-nestjs-application-with-nginx-on-ubuntu 
```sh
sudo npm install -g @nestjs/cli
nest new my-nest-app
cd my-nest-app

npm run start
```


## Main Documentation
1. Set up NestJS Backend
First, create a NestJS application if you haven't already:
```bash
npm i -g @nestjs/cli
nest new my-nest-app
```
Create a simple endpoint in your NestJS application. For example, add the following code to the app.controller.ts file:

```typescript

import { Controller, Get } from '@nestjs/common';

@Controller('api')
export class AppController {
  @Get('hello')
  getHello(): string {
    return 'Hello from NestJS!';
  }
}
```
Ensure your NestJS server is running:

```bash

npm run start
```
2. Set up Next.js Frontend
Create a Next.js application if you haven't already:

```bash

npx create-next-app@latest my-next-app
cd my-next-app
```
Install Axios (or any other HTTP client you prefer):

```bash

npm install axios
```
3. Connect Next.js to NestJS
Create a component or page in your Next.js application that will fetch data from the NestJS API. For example, add the following code to pages/index.js:

```javascript

import { useEffect, useState } from 'react';
import axios from 'axios';

export default function Home() {
  const [message, setMessage] = useState('');

  useEffect(() => {
    const fetchMessage = async () => {
      try {
        const response = await axios.get('http://localhost:3000/api/hello');
        setMessage(response.data);
      } catch (error) {
        console.error('Error fetching message:', error);
      }
    };

    fetchMessage();
  }, []);

  return (
    <div>
      <h1>Next.js to NestJS Example</h1>
      <p>{message}</p>
    </div>
  );
}
```
4. Run Both Applications
Ensure your NestJS server is running:

```bash

cd my-nest-app
npm run start
```
Then, run your Next.js development server:

```bash

cd my-next-app
npm run dev
```

# Ping from NestJs to Database
1. Install Dependencies
First, you need to install the necessary dependencies:

```bash

npm install @nestjs/typeorm typeorm mysql2
```
2. Configure TypeORM in NestJS
Open the app.module.ts file and update it to configure TypeORM to connect to your MySQL database:

```typescript

import { Module } from '@nestjs/common';
import { TypeOrmModule } from '@nestjs/typeorm';
import { AppController } from './app.controller';
import { AppService } from './app.service';

@Module({
  imports: [
    TypeOrmModule.forRoot({
      type: 'mysql',
      host: 'localhost', // Your database host
      port: 3306, // Your database port
      username: 'root', // Your database username
      password: 'password', // Your database password
      database: 'test', // Your database name
      entities: [],
      synchronize: true,
    }),
  ],
  controllers: [AppController],
  providers: [AppService],
})
export class AppModule {}
```
3. Create a Service to Ping the Database
Create a simple service that uses the TypeORM connection to ping the database. Create a file named ping.service.ts:

```typescript

import { Injectable } from '@nestjs/common';
import { InjectConnection } from '@nestjs/typeorm';
import { Connection } from 'typeorm';

@Injectable()
export class PingService {
  constructor(
    @InjectConnection()
    private readonly connection: Connection,
  ) {}

  async pingDatabase(): Promise<boolean> {
    try {
      await this.connection.query('SELECT 1');
      return true;
    } catch (error) {
      return false;
    }
  }
}
```
4. Create a Controller to Handle Ping Request
Create a controller that exposes an endpoint to ping the database. Create a file named ping.controller.ts:

```typescript

import { Controller, Get } from '@nestjs/common';
import { PingService } from './ping.service';

@Controller('ping')
export class PingController {
  constructor(private readonly pingService: PingService) {}

  @Get()
  async ping(): Promise<string> {
    const isDatabaseConnected = await this.pingService.pingDatabase();
    return isDatabaseConnected ? 'Database is connected!' : 'Failed to connect to the database.';
  }
}
```
5. Update App Module
Finally, update the app.module.ts to include the newly created PingService and PingController:

```typescript

import { Module } from '@nestjs/common';
import { TypeOrmModule } from '@nestjs/typeorm';
import { AppController } from './app.controller';
import { AppService } from './app.service';
import { PingService } from './ping.service';
import { PingController } from './ping.controller';

@Module({
  imports: [
    TypeOrmModule.forRoot({
      type: 'mysql',
      host: 'localhost',
      port: 3306,
      username: 'root',
      password: 'password',
      database: 'test',
      entities: [],
      synchronize: true,
    }),
  ],
  controllers: [AppController, PingController],
  providers: [AppService, PingService],
})
export class AppModule {}
```
6. Run the Application
Ensure your MySQL server is running and then start your NestJS application:

```bash

npm run start
```

# 
1. Install MySQL
If you don't already have MySQL installed, you need to install it. You can download MySQL from the official MySQL website.

2. Start MySQL Server
After installation, start the MySQL server. The command to start MySQL may vary depending on your operating system.

sudo service mysql start
3. Access MySQL Command Line
Access the MySQL command line client using the following command and log in as the root user:

```bash

mysql -u root -p
```
4. Create Database
Once you're logged in to the MySQL command line client, create a database named test (or any other name you prefer, but make sure it matches the name in your NestJS configuration).

```sql

CREATE DATABASE test;
```
5. Create User (Optional)
If you want to create a specific user for your application instead of using the root user, you can do so with the following commands. Replace 'your_password' with a strong password.

```sql

CREATE USER 'nest_user'@'localhost' IDENTIFIED BY 'your_password';
GRANT ALL PRIVILEGES ON test.* TO 'nest_user'@'localhost';
FLUSH PRIVILEGES;
```
Update your NestJS configuration accordingly:

```typescript

TypeOrmModule.forRoot({
  type: 'mysql',
  host: 'localhost',
  port: 3306,
  username: 'nest_user', // New user
  password: 'your_password', // New user's password
  database: 'test',
  entities: [],
  synchronize: true,
}),
```

# Conect from NestJs to Database and add data

1. Ensure Data is Inserted into the Database
Verify if the data is correctly inserted into your MySQL database.

Using MySQL Command Line:
Connect to your MySQL server:

```bash

mysql -u root -p
```
Enter your password when prompted.

Switch to the test database:

```sql

USE test;
```
Check the contents of the User table:

```sql

SELECT * FROM User;
```
If the table is empty, insert some test data:

```sql

INSERT INTO User (name, email) VALUES ('John Doe', 'john.doe@example.com');
INSERT INTO User (name, email) VALUES ('Jane Smith', 'jane.smith@example.com');
```
2. Ensure Your NestJS Application is Correctly Configured
Make sure your entity, service, and controller are set up correctly.

user.entity.ts
```typescript

import { Entity, Column, PrimaryGeneratedColumn } from 'typeorm';

@Entity()
export class User {
  @PrimaryGeneratedColumn()
  id: number;

  @Column()
  name: string;

  @Column()
  email: string;
}
user.service.ts
typescript

import { Injectable } from '@nestjs/common';
import { InjectRepository } from '@nestjs/typeorm';
import { Repository } from 'typeorm';
import { User } from './user.entity';

@Injectable()
export class UserService {
  constructor(
    @InjectRepository(User)
    private usersRepository: Repository<User>,
  ) {}

  findAll(): Promise<User[]> {
    return this.usersRepository.find();
  }

  create(name: string, email: string): Promise<User> {
    const user = this.usersRepository.create({ name, email });
    return this.usersRepository.save(user);
  }
}
```
user.controller.ts
```typescript

import { Controller, Get, Post, Body } from '@nestjs/common';
import { UserService } from './user.service';
import { User } from './user.entity';

@Controller('users')
export class UserController {
  constructor(private readonly userService: UserService) {}

  @Get()
  async findAll(): Promise<User[]> {
    const users = await this.userService.findAll();
    console.log(users); // Print data to console
    return users;
  }

  @Post()
  async create(@Body() body: { name: string; email: string }): Promise<User> {
    const user = await this.userService.create(body.name, body.email);
    console.log(user); // Print the created user to console
    return user;
  }
}
```
app.module.ts
```typescript

import { Module } from '@nestjs/common';
import { TypeOrmModule } from '@nestjs/typeorm';
import { AppController } from './app.controller';
import { AppService } from './app.service';
import { User } from './user.entity';
import { UserService } from './user.service';
import { UserController } from './user.controller';

@Module({
  imports: [
    TypeOrmModule.forRoot({
      type: 'mysql',
      host: 'localhost',
      port: 3306,
      username: 'root',
      password: 'password',
      database: 'test',
      entities: [User],
      synchronize: true,
    }),
    TypeOrmModule.forFeature([User]),
  ],
  controllers: [UserController],
  providers: [UserService],
})
export class AppModule {}
```
3. Add Data via NestJS Endpoint
If no data is present in the database, add some data using the NestJS POST endpoint:

```bash

curl -X POST http://localhost:3001/users -H "Content-Type: application/json" -d '{"name":"Alice Johnson","email":"alice.johnson@example.com"}'
```
Then, check again by running:

```bash

curl http://localhost:3001/users
```
