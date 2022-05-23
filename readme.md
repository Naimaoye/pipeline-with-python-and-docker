#### About data engineering
You might heard of Docker-compose. The difference between Docker and Docker-compose is simple: docker commands are focused on only one container (or image) at once while docker-compose manage several containers docker.

#### Scripts
```
docker run -it \
  -e POSTGRES_USER="root" \
  -e POSTGRES_PASSWORD="root" \
  -e POSTGRES_DB="ny_taxi" \
  -v /c/Users/44784/Documents/Projects/docker-example/ny_taxi_postgres_data:/var/lib/postgresql/data \
  -p 5431:5432 \
  postgres:13

```

```
https://www1.nyc.gov/site/tlc/about/tlc-trip-record-data.page
https://s3.amazonaws.com/nyc-tlc/trip+data/yellow_tripdata_2021-01.csv
docker pull dpage/pgadmin4

```


### Creating network:

```
docker network create <network name>

```

```
docker run -it \
  -e POSTGRES_USER="root" \
  -e POSTGRES_PASSWORD="root" \
  -e POSTGRES_DB="ny_taxi" \
  -v /c/Users/44784/Documents/Projects/docker-example/ny_taxi_postgres_data:/var/lib/postgresql/data \
  -p 5431:5432 \
  --network=pg-network-2
  --name pg-database-2
  postgres:13


#PGAdmin
docker run -it -e PGADMIN_DEFAULT_EMAIL="admin@admin.com" -e PGADMIN_DEFAULT_PASSWORD="root" -p 8080:80 --network=pg-network-2 --name pgadmin dpage/pgadmin4

URL="https://s3.amazonaws.com/nyc-tlc/trip+data/yellow_tripdata_2021-01.csv"
python ingest_data.py --user=root --password=root --host=localhost --port=5432 --db=ny_taxi --table_name=yellow_taxi_trips --url=${URL}

#Using python scripts
python ingest_data.py
  --user=root \
  --password=root \
  --host=localhost \
  --port=5432 \
  --db=ny_taxi \
  --table_name=yellow_taxi_trips \
  --url=${URL}

#Throwing error but this came to the rescue
python3 -m pip install pandas

```
### Using docker image:
We just need to run 

```
docker build -t <name> <path to dockerfile>

```
Then we run:
```
docker run <image name> <{pass all the params i.e user, password etc}>

```
### Using docker compose:
- setup docker-compose.yaml file with database name, pgadmin name and ports
- RUN docker-compose up 
