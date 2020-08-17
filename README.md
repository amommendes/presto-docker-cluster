## Presto cluster with docker

- 1. Download source tar.gz and cli from [here](https://prestosql.io/download.html) and put in `docker/src` 
- 2. Build prestosql image from docker folder. You can change prestosql version setting the `ARG` PRESTO_VERSION when building. Default is 340.
```
docker build -t prestosql .
```
- 3. Up coordinator service
```
docker-compose up -d coordinator 
```
- 4. After coodinator is up and running. Up workers
```
docker-compose up -d --scale worker=2 
```