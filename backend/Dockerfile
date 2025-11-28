FROM node:18-alpine

WORKDIR /usr/src/app

# install dependencies (production only)
COPY package*.json ./
RUN npm install --production --silent

# copy app source
COPY . .

ENV NODE_ENV=production

# default port used by the app (see server.js)
EXPOSE 8080

# start the server
CMD ["node", "server.js"]
