# download a base version of node from Docker Hub
FROM node:alpine
# Update packages on node image
RUN cat /etc/resolv.conf
RUN apk -U upgrade --no-cache
# create the working directory for the application called /app that will be the root
WORKDIR /app
EXPOSE 5000
# COPY ./package.json package.json 
# npm install the dependencies and run the start script from each package.json
# RUN ls -ltr && npm install && npm update 
COPY . .
# RUN mkdir -p /app/uploads/images && \ 
#     touch /app/uploads/images/README.md && \
#     ls -lh /app/uploads/images
RUN ls -ltr && npm install -g npm@7.10.0 &&  npm install && npm update
CMD npm start