FROM node:17.0.1-alpine as build

WORKDIR /usr/src/app

ARG NPM_TOKEN

COPY package*.json yarn.lock ./

RUN yarn install

COPY . .

RUN yarn build

FROM node:17.0.1-alpine

WORKDIR /usr/src/app

COPY --from=build /usr/src/app/node_modules ./node_modules
COPY --from=build /usr/src/app/dist ./dist

CMD ["node", "dist/main"]
