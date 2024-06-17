![Alt texts](../Images/p1.png)
# Day 104 | Use EC2 Ubuntu setup Full stack NextJS + NestJS
# Setup EC2 Ubuntu

# Install Node v20
Link: https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-22-04 
```sh
node -v
npm -v
```
# Setup NextJS
Link: https://www.digitalocean.com/community/developer-center/deploying-a-next-js-application-on-a-digitalocean-droplet
```sh
npx create-next-app my-next-app
cd my-next-app

npm start


```
# Setup NestJS
Link: https://www.digitalocean.com/community/tutorials/how-to-deploy-a-nestjs-application-with-nginx-on-ubuntu 
```sh
sudo npm install -g @nestjs/cli
nest new my-nest-app
cd my-nest-app

npm run start
```