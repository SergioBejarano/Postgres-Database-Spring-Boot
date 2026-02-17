## Guía de ejecución

### Requisitos

- Java 17+
- Maven 3.9+
- PostgreSQL 15 instalado localmente

### Configurar PostgreSQL local

1. Asegúrate de que el servicio escuche en `localhost` con `port = 5433`. Si decides mantener 5432, actualiza el valor en `src/main/resources/application.properties`.
2. Reinicia PostgreSQL tras cualquier cambio de puerto.
3. Crea la base de datos, el usuario y los permisos que la aplicación espera:

```sql
CREATE DATABASE midb;
CREATE USER "user" WITH ENCRYPTED PASSWORD 'pass';
GRANT ALL PRIVILEGES ON DATABASE midb TO "user";
ALTER DATABASE midb OWNER TO "user";
GRANT ALL ON SCHEMA public TO "user";
```

4. Verifica la conexión con `psql -h localhost -p 5433 -U user -d midb`.

> Si cambias el nombre de la base, usuario, contraseña o puerto, recuerda mantener sincronizado `spring.datasource.*` en `application.properties`.

### Ejecutar la aplicación

```sh
mvn clean spring-boot:run
```

La API quedará disponible en `http://localhost:8081`. El endpoint actual para probar es `POST /v1/user` con un cuerpo JSON como:

```json
{
  "name": "sergio",
  "email": "sergio@mail.com"
}
```

Puedes consultar usuarios creados con `GET /v1/user/{id}`.
