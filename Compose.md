For larger projects that require multiple services, manually managing individual docker containers 
becomes a pain very quickly. As an example, we could be building a backend for an app, and may require 
the following containers:

- PostgreSQL
- Adminer (a database management service)
- Redis (caching service)
- ...

We'd have to do something like this:
```
# start postgres
docker run -d postgres:alpine

# start redis
docker run -d redis

# start adminer
docker run -p 8080:8080 adminer

# more commands if you have more container requirements
... 
```

As you'd imagine, running this multiple times quickly becomes cumbersome. 

# Docker Compose
Docker Compose is a separate tool (although usually packaged with Docker) that allows us to define a 
multi-container docker setup in just one file. 

With Docker Compose, we can define all of these services in `compose.yaml`:

```yaml
services:
  postgres:
    image: postgres:alpine

  redis:
    image: redis

  adminer:
    image: adminer
    ports:
      - "8080:8080"

volumes:
  postgres_data:
```

Then, we can run the file (and all services defined within it) using `docker compose up`, 
or `docker compose -f <file> up` if you chose not to name your file `compose.yaml`.

To stop all the containers, simply run `docker compose down` in another terminal, or `ctrl-c` in the same terminal
you ran it in, to send a kill signal to the Docker Compose process. 
