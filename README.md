# Pizza Hunt

## Features

- Perfect setup for an AWS EC2 instance
- Local Mongodb database
- Ngrok tunnel for a secure, over-the-air connection to localhost:3001 (free!)
- Uncomplicated (no React!)
- Amazon Route 53 compatible for domain connection

## Setup on AWS

- Use Ubuntu 22, give 30GB (free!)
- Create pair for ssh
- SSH into machine
- Install ngrok:
```
curl -s https://ngrok-agent.s3.amazonaws.com/ngrok.asc | sudo tee /etc/apt/trusted.gpg.d/ngrok.asc >/dev/null && echo "deb https://ngrok-agent.s3.amazonaws.com buster main" | sudo tee /etc/apt/sources.list.d/ngrok.list && sudo apt update && sudo apt install ngrok
```
- Install mongodb:
```
wget https://repo.mongodb.org/apt/ubuntu/dists/jammy/mongodb-org/6.0/multiverse/binary-amd64/mongodb-org-server_6.0.7_amd64.deb
sudo dpkg -i mongodb-org-server_6.0.7_amd64.deb
sudo rm -r mongodb-org-server_6.0.7_amd64.deb
```
- Install node:
```
wget https://nodejs.org/dist/v20.4.0/node-v20.4.0-linux-x64.tar.xz
sudo tar -xvf node-v20.4.0-linux-x64.tar.xz
sudo cp -r node-v20.4.0-linux-x64/{bin,include,lib,share} /usr/
export PATH=/usr/node-v20.4.0-linux-x64/bin:$PATH
sudo rm -r node-v20.4.0-linux-x64.tar.xz
sudo rm -r node-v20.4.0-linux-x64
```

## Usage

Spin up db:

```
cd pizza-hunt
sudo mongod --fork --logpath /var/log/mongod.log --dbpath ./data/db
```

Develop:

`npm run dev`

```bash
> nosql@1.0.0 dev
> node dev.js

Server now available at https://REDACTED.ngrok-free.app
🌍 Connected on http://localhost:3001
Mongoose: pizzas.find({}, { sort: { _id: -1 }, projection: { __v: 0 } })
Mongoose: pizzas.find({}, { sort: { _id: -1 }, projection: { __v: 0 } })
Mongoose: pizzas.insertOne({ pizzaName: 'rewarew', createdBy: 'fdsaf', size: 'Extra Large', toppings: [ 'Bacon' ], comments: [], _id: new ObjectId("64a6b21b3a9c69a8acbfc021"), createdAt: new Date("Thu, 06 Jul 2023 12:22:51 GMT"), __v: 0}, { session: null })
Mongoose: pizzas.find({}, { sort: { _id: -1 }, projection: { __v: 0 } })
```
