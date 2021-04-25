# download a base version of node from Docker Hub
FROM node:alpine
# Update packages on node image
RUN cat /etc/resolv.conf
RUN apk -U upgrade --no-cache
# create the working directory for the application called /app that will be the root
WORKDIR /app
COPY ./package.json package.json 
# npm install the dependencies and run the start script from each package.json
RUN ls -ltr && npm install -g npm@7.10.0 && npm install && npm update
COPY . .
# EXPOSE 3000
# RUN npm audit fix --force
CMD npm start