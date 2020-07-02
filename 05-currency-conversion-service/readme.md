# Currency Conversion Micro Service

Run CurrencyConversionServiceApplication as a Java Application.

## Containerization

### Troubleshooting

- Problem - Caused by: com.spotify.docker.client.shaded.javax.ws.rs.ProcessingException: java.io.IOException: No such file or directory
- Solution - Check if docker is up and running!
- Problem - Error creating the Docker image on MacOS - java.io.IOException: Cannot run program “docker-credential-osxkeychain”: error=2, No such file or directory
- Solution - https://medium.com/@dakshika/error-creating-the-docker-image-on-macos-wso2-enterprise-integrator-tooling-dfb5b537b44e

### Creating Containers

- mvn package

### Running Containers

```
docker network create currency-network
For any container already running, add them to the network
docker network connect currency-network <container-id>
For any image that needs to be run i.e. container not already created - docker run --network option
docker run --detach --publish 3306:3306 --network currency-network --name mysql --env MYSQL_ROOT_PASSWORD=dummypassword --env MYSQL_USER=exchange-db-user --env MYSQL_PASSWORD=dummyexchange --env MYSQL_DATABASE=exchange-db --name mysql  mysql:5.7
docker run --detach --publish 8000:8000 --network currency-network --name currency-exchange-microservice  --env RDS_HOSTNAME=mysql gspear/aws-currency-exchange-service-mysql:0.0.1-SNAPSHOT
docker run --detach --publish 8100:8100 --network currency-network --name currency-conversion-microservice --env CURRENCY_EXCHANGE_URI=http://currency-exchange-microservice:8000 gspear/aws-currency-conversion-service:0.0.1-SNAPSHOT
```
```
Running with docker-compose
docker-compose-up will run the yaml that will create the three containers and their dependencies.
```
#### Test API 
- http://localhost:8100/api/currency-conversion-microservice/currency-converter/from/EUR/to/INR/quantity/10
```
docker login
docker push gspear/aws-currency-conversion-service:0.0.1-SNAPSHOT
```


## Resources

- http://localhost:8100/api/currency-conversion-microservice/currency-converter/from/EUR/to/INR/quantity/10

```json
{
id: 10002,
from: "EUR",
to: "INR",
conversionMultiple: 75,
quantity: 10,
totalCalculatedAmount: 750,
exchangeEnvironmentInfo: "NA",
conversionEnvironmentInfo: "NA",
}
```