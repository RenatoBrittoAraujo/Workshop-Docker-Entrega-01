FROM node:16-alpine As development

RUN mkdir /app

WORKDIR /app

COPY package*.json ./

RUN yarn

COPY . .

CMD ["yarn", "watch"]

FROM node:16-alpine as production

ARG NODE_ENV=production
ENV NODE_ENV=${NODE_ENV}

WORKDIR /app

COPY package*.json ./

RUN npm install --only=production

COPY . .

COPY --from=development /app/dist ./dist

CMD ["node", "dist/index.js"]