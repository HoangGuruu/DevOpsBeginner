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

