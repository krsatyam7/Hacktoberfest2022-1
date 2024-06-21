# stage one
FROM node:20.14.0-alpine3.20 as builder

# install dependencies for node-gyp
RUN apk add --no-cache python2 make g++

WORKDIR /app

COPY ./package.json .
RUN npm install --only=prod

# stage two
FROM node:20.14.0-alpine3.20

EXPOSE 3000
ENV NODE_ENV=production

USER node
RUN mkdir -p /home/node/app
WORKDIR /home/node/app

COPY . .
COPY --from=builder /app/node_modules  /home/node/app/node_modules

CMD [ "node", "bin/www" ]
