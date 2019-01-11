# Run SonarQube with a PostgreSQL database

Create this `docker-compose.yml` file

```yaml
sonarqube:
  image: sonarqube
  ports:
   - "9000:9000"
   - "5432:5432"
  links:
    - db:db
  environment:
   - SONARQUBE_JDBC_URL=jdbc:postgresql://db:5432/sonar

db:
  image: postgres
  environment:
   - POSTGRES_USER=sonar
   - POSTGRES_PASSWORD=sonar
```

Use [docker-compose](https://github.com/docker/compose) to start the containers.

```bash
$ docker-compose up -d
```

Analyse a project:

```bash
mvn sonar:sonar \
  -Dsonar.host.url=http://$(docker-machine ip):9000 \
  -Dsonar.jdbc.url=jdbc:postgresql://$(docker-machine ip)/sonar
```

## To be improved

 + Backup
 + Clustering
 + Upgrade
 + Admin password
 + Plugins
 + ...
