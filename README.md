# Oauth2-Jwt-Auth
## OAuth2 JWT Provider & Resource Server

This sample demonstrates how to accept JWTs without using a separate authorization server.

This approach is useful in REST APIs when a user would like to locally authenticate with a username and password and then use a JWT thereafter.

## Running the Application

To run the application, use the following command:

```bash
mvn spring-boot:run
```

This will start the application on http://localhost:8081.

Requesting a Token

To obtain a JWT, send a POST request to the /token endpoint with the username - user and the password - password. You can use curl to request the token:

```bash
curl -i -X POST user:password@localhost:8081/token
```

The server will respond with a JWT token similar to the following:

```bash
eyJhbGciOiJSUzI1NiJ9.eyJpc3MiOiJzZWxmIiwic3ViIjoidXNlciIsImV4cCI6MTYwNDA0MzA1MSwiaWF0IjoxNjA0MDA3MDUxfQ.yDF_JgSwl5sk21CF7AE1AYbYzRd5YYqe3MIgSWpgN0t2UqsjaaEDhmmICKizt-_0iZy8nkEpNnvgqv5bOHDhs7AXlYS1pg8dgPKuyfkhyVIKa3DhuGyb7tFjwJxHpr128BXf1Dbq-p7Njy46tbKsZhP5zGTjdXlqlAhR4Bl5Fxaxr7D0gdTVBVTlUp9DCy6l-pTBpsvHxShkjXJ0GHVpIZdB-c2e_K9PfTW5MDPcHekG9djnWPSEy-fRvKzTsyVFhdy-X3NXQWWkjFv9bNarV-bhxMlzqhujuaeXJGEqUZlkhBxTsqFr1N7XVcmhs3ECdjEyun2fUSge4BoC7budsQ
```

So, next, request the token and export it:

```bash
export TOKEN=`curl -XPOST user:password@localhost:8081/token`
```

Finally, request `/`, including the bearer token for authentication:

```bash
curl -H "Authorization: Bearer $TOKEN" localhost:8081 && echo
```

You should see a response like:

```bash
Hello, user!
```
