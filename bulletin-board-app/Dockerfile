FROM node:18-alpine

WORKDIR /usr/src/app

# Copy package.json + package-lock.json
COPY package*.json ./

RUN npm install --only=production

# Copy rest of app code
COPY . .

EXPOSE 8080

CMD ["npm", "start"]
