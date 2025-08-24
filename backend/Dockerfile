FROM node:20-alpine AS base
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
COPY . .
EXPOSE 8080
ENV NODE_ENV=production
ENV MONGO_URL=mongodb://mongo:27017/dd_db
CMD ["node", "server.js"]
