#make service up from file

```docker-compose -f mysql-compose.yml up```

or 

```docker compose -f mysql-compose.yml up` -d```


#make service down from file

```docker-compose -f mysql-compose.yml down```

### Scale docker compose
   `docker-compose up --scale petstore=3`
