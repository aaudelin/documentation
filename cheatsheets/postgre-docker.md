sudo docker run -d -e POSTGRES_USER=postgres -e POSTGRES_PASSWORD=mysecretpassword --name postgres-server -p 5432:5432 -v pgdata:/var/lib/postgresql/data --restart=always postgres

sudo docker run -p 2589:80 -e "PGADMIN_DEFAULT_EMAIL=user@domain.com" -e "PGADMIN_DEFAULT_PASSWORD=SuperSecret" -d dpage/pgadmin

sudo docker inspect postgres-server
