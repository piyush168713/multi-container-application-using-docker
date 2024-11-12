npm install
node app.js

docker build -t backend:v2 .



Your host machine is using port 80.  You will have to forward your container to another port on your host.

1) change the forwarded port to 8080 in your run command,  docker run --name goals-backend --rm -d -p 8080:80 backend:v1

2) In the frontend application, in App.js, you will need to change all instances making requests to use port 8080

    fetch('http://localhost:8080/goals/')



-- Using basic docker server
-- with host.docker.internal in app.js(backend)
docker run --name goals-backend --rm -d -p 8080:80 backend:v5
Image - piyush168173/demo-app:backendv5




-- Using Network
-- with mongodb in app.js(backend)
docker run --name goals-backend --rm -d -p 8080:80 --network goals-net backend:v2
Image - piyush168173/demo-app:backendv2


-- Using Volume
-- with max:secret@mongodb:27017 in app.js(backend)
- run this container under /backend dir coz of $(pwd)
docker run --name goals-backend -v $(pwd):/app -v logs:/app/logs -v /app/node_modules --rm -d -p 8080:80 --network goals-net backend:v3
Image - piyush168173/demo-app:backendv3