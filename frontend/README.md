npm install

npm start



Your host machine is using port 80.  You will have to forward your container to another port on your host.

1) change the forwarded port to 8080 in your run command,  docker run --name goals-backend --rm -p 8080:80 backend:v1

2) In the frontend application, in App.js, you will need to change all instances making requests to use port 8080

    fetch('http://localhost:8080/goals/')



docker build -t frontend:v1 .


-- Using basic docker server
-- with host.docker.internal in app.js(backend)
docker run --name goals-frontend --rm -p 3000:3000 -it -d frontend:v1


-- Using Network
-- with mongodb in app.js(backend)
docker run --name goals-frontend --rm -p 3000:3000 -it -d frontend:v1


-- Using Volume
-- with max:secret@mongodb:27017 in app.js(backend)
docker run --name goals-frontend --rm -p 3000:3000 -it -d frontend:v1


Image pushed - piyush168713/demo-app:v1