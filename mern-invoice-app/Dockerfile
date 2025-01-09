FROM node:18 AS build
WORKDIR /usr/src/app
COPY mern-invoice-app/package*.json ./
RUN npm install
COPY backend/ .

FROM node:18-slim
WORKDIR /usr/src/app
COPY --from=build /usr/src/app .
EXPOSE 5000
CMD ["npm", "start"]
