run redis
=====
docker run --name eapps-redis -p 6379:6379 -d redis

cli terminal
=====
docker exec -it eapps-redis redis-cli

Command
===
keys *

GET order::1

DEL KEYS Order
