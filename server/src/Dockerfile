FROM node as builder
# Create app directory
WORKDIR /usr/src/app
# Install app dependencies
COPY package.json package-lock ./
RUN npm i 
COPY . .
RUN npm build

FROM node:slim
# Create app directory
WORKDIR /usr/src/app
COPY package.json package-lock ./
RUN npm ci --production

COPY --from=builder /usr/src/app/dist ./dist

EXPOSE 3001
CMD [ "node", "dist/index.js" ]