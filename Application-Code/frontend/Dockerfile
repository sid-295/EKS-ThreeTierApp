FROM node:14 AS builder

WORKDIR /app

COPY package*.jason ./

RUN npm install

COPY . .

FROM node:14-slim

WORKDIR /app

COPY --from=builder /app /app

RUN npm install --production 

CMD ["npm" , "start"]
