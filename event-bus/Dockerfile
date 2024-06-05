FROM node:14

WORKDIR /i211233_Backend

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 3233 
 # 1233+ 2000 
CMD ["node", "src/server.js"]