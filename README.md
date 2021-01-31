# ledger-root

helm repo add bitnami https://charts.bitnami.com/bitnami

helm dependency update k8s/postgres/
helm dependency update k8s/redis/
helm dependency update k8s/kafka/


# local development
after starting docker-compose run in terminal:
```yaml
curl -i -X POST -H "Accept:application/json" -H "Content-Type:application/json" localhost:8083/connectors/ -d '{
  "name": "lg-acc-conn",  
  "config": {
    "connector.class": "io.debezium.connector.postgresql.PostgresConnector", 
    "database.hostname": "ledger-pg", 
    "database.port": "5432", 
    "database.user": "postgres", 
    "database.password": "", 
    "database.dbname" : "ledger-accounting", 
    "database.server.name": "lg-accounting", 
    "table.include.list": "public.a2u,public.accounts,public.users",
    "plugin.name": "pgoutput"
  }
}'
```