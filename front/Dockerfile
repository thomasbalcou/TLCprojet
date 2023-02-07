#1: Compile et Build le code angular

#node image comme base image
FROM node:16.19.0 as build
#working directory
WORKDIR /app
#ajoute le contenu du dossier front dans le dossier app du docker
COPY ./ /app/
# Install les dependances
RUN npm install
# build app
RUN npm run build
#RUN npm run build

#2: Serve app with nginx server
# nginx image comme base image
FROM nginx:latest

# Copy the build output to replace the default nginx contents.
COPY --from=build /app/dist/tlcfront /usr/share/nginx/html

#docker build -t front .
#docker run -d -p 8080:80 front
