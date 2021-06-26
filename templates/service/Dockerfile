FROM node:16.3.0-alpine as build

WORKDIR /usr/src/app

ARG NPM_TOKEN

COPY package*.json yarn.lock ./

RUN echo "@indivorg:registry=https://npm.pkg.github.com" > .npmrc
RUN echo "//npm.pkg.github.com/:_authToken=$NPM_TOKEN" >> .npmrc

RUN yarn install
RUN rm -f .npmrc

COPY . .

RUN yarn build

FROM node:16.3.0-alpine

WORKDIR /usr/src/app

COPY --from=build /usr/src/app/node_modules ./node_modules
COPY --from=build /usr/src/app/dist ./dist

CMD ["node", "dist/main"]