# Challenge2DockerFundamentals

This is challenge number 2 in the Docker Fundamentals course by [Gelopfalcon](https://www.instagram.com/gelopfalcon/)

**Commands Used**

First, create a volume to store the data of the frontend app.

  `docker volume create pgdata`
  
  `docker run --name postgres -e POSTGRES_PASSWORD=12345 -d -p 5432:5432 -v  pgdata:/var/lib/postgresql/data postgres`

Then, we need to create our network

`docker network create teemii-network -d bridge`

Now, we're gonna pull the backend container

`docker run --name=teemii-backend --env=POSTGRES_HOST=postgres --env=POSTGRES_USER=postgres --env=POSTGRES_PASSWORD=12345 --env=POSTGRES_DB=postgres -p 3000:3000 -d dokkaner/teemii-backend:develop`

Finally, we need to pull the frontend container

`docker run --name=teemii-frontend -p 8080:80 -d dokkaner/teemii-frontend:develop`

At this point, we have our volume and backend running. You can check in Docker Desktop.

Our next step is to connect our containers.

`docker network connect teemii-network postgres`

`docker network connect teemii-network teemii-backend`

`docker network connect teemii-network teemii-frontend`

Our final step is run the frontend app

`docker start teemii-frontend`

All set! We've finished the challenge 😄.
