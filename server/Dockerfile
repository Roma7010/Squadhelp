FROM node:14.16.1-alpine3.13 

ARG NODE_ENV="development"

RUN mkdir /server

RUN mkdir -p /var/www/html/images

WORKDIR /server

COPY package*.json ./

RUN npm install -g nodemon
RUN npm install -g sequelize-cli



RUN npm install

COPY . .

EXPOSE 3000

CMD sequelize db:migrate && sequelize db:seed:all && npm start





FROM node:14.16.1-alpine3.13 as debug

ARG NODE_ENV="development"

RUN mkdir /server

RUN mkdir -p /var/www/html/images

WORKDIR /server

COPY package*.json ./

RUN npm install -g nodemon
RUN npm install -g sequelize-cli

COPY ./src /server/src/

ENTRYPOINT [ "nodemon","--inspect=127.0.0.1","./src/index.js" ]

RUN npm install

COPY . .

EXPOSE 3000

CMD sequelize db:migrate && sequelize db:seed:all && npm start
