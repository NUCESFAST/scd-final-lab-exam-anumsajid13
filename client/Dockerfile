FROM node:14 as build

RUN apt-get update && apt-get install -y curl

WORKDIR /i211233_Frontnd

COPY package*.json ./

RUN npm install

RUN npm install -g serve

COPY . .

RUN npm run build

EXPOSE 1233

CMD ["serve", "-s", "build"]