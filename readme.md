Three Container will run:

1- Database - Mongodb
    - Data must persist
    - Access will be limited
	docker run --name mongodb -d -p 27017:27017 mongo

2. Backend - NodeJS REST API
    - Data must persist
    - Live source code update

3. Frontend - React SPA
    - Live source code update




-- we use host.docker.internal instead of mongodb in app.js(backend)
-- now container will communicate with ports not with network

docker run --name mongodb -d -p 27017:27017 mongo

docker run --name goals-backend --rm -d -p 8080:80 backend:v5

docker run --name goals-frontend --rm -d -p 3000:3000 -it frontend:v1

- Image pushed to dockerhub
    1. docker pull piyush168713/demo-app:backendv5






-- Creating Network (l-85)
    now container will communicate with network not with ports
docker network create goals-net

- docker run --name mongodb --rm -d --network goals-net mongo

- docker run --name goals-backend --rm -d -p 8080:80 --network goals-net backend:v2
    - so we use name of mongo container (mongodb) instead of host.docker.internal in app.js(backend)
    - so build the backend image again (docker build -t backend:v2 .)

- docker run --name goals-frontend --rm -p 3000:3000 -it -d frontend:v1

- Image pushed to dockerhub
    1. docker pull piyush168713/demo-app:backendv2
    2. docker pull piyush168713/demo-app:frontendv1





-- Creating Volumes (l-87)
docker run --name mongodb -v data:/data/db --rm -d --network goals-net -e MONGO_INITDB_ROOT_USERNAME=max -e MONGO_INITDB_ROOT_PASSWORD=secret mongo
    for using id and password, we need to do some change in app.js(backend) and rebuilt the backend image
    changes -> 'mongodb://max:secret@mongodb:27017/course-goals?authSource=admin',


- run this container under /backend dir coz of $(pwd)
docker run --name goals-backend -v $(pwd):/app -v logs:/app/logs -v /app/node_modules --rm -d -p 8080:80 --network goals-net backend:v3
    If you face MongoError: Authentication failed. this problem then stop the container and remove the named v volume you created then start the container again. (docker volume ls) (docker volume rm data)

docker run --name goals-frontend --rm -p 3000:3000 -it -d frontend:v1


- Image pushed to dockerhub
    1. docker pull piyush168713/demo-app:backendv3
    2. docker pull piyush168713/demo-app:frontendv1