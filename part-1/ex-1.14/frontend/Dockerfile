FROM node:16-bullseye-slim

EXPOSE 5000

WORKDIR /app

COPY package*.json ./

EXPOSE 5000
ENV REACT_APP_BACKEND_URL=http://localhost:8080

RUN npm install

COPY . .

RUN npm run build

RUN npm install -g serve

CMD ["serve", "-s", "-l", "5000", "build"]
