# JWT Login Sample

## JWT Authentication in a Monolithic Application with OAuth2 Resource Server and Nimbus JOSE

This project demonstrates how to use Spring Security OAuth2 Resource Server to validate JWTs without writing custom filters. For token generation and verification, the Nimbus JOSE + JWT library is used, providing a secure and convenient integration of JWT authentication in monolithic applications.

## Features

### Authentication and Token Generation
- Users authenticate using a basic scheme (username/password).
- After successful authentication, the server generates a JWT token containing the user's information and authorities.

### Token Validation
- Spring Security OAuth2 Resource Server automatically validates JWTs for each request.
- No custom filters are required—everything is handled via standard Spring configuration.

### Simple REST API
- **GET /** – Returns a greeting with the authenticated user's name.
- **POST /token** – Generates and returns a JWT token.

## Technologies

- **Spring Boot** — The primary framework for development.
- **Spring Security OAuth2 Resource Server** — For processing and validating JWT tokens.
- **Nimbus JOSE + JWT** — For generating, signing, and verifying JWT tokens.
- **In-Memory Authentication** — Simple authentication using InMemoryUserDetailsManager.

## Running the Project

Clone the repository:

```bash
git clone https://github.com/Dmitrii-Russu/jwt-login-sample.git
cd spring-academy-rest-api
```

Run the application with Maven:

```bash
mvn spring-boot:run
```

The application will start at http://localhost:8081.

## Using the Endpoints

1. Generating a JWT Token
Send a POST request to the /token endpoint with the credentials (user/password):

```bash
curl -i -X POST -u "user:password" http://localhost:8081/token
```

You will receive a JWT token similar to the following:

```bash
eyJhbGciOiJSUzI1NiJ9.eyJpc3MiOiJzZWxmIiwic3ViIjoidXNlciIsImV4cCI6MTYwNDA0MzA1MSwiaWF0IjoxNjA0MDA3MDUxfQ.yDF_JgSwl5sk21CF7AE1AYbYzRd5YYqe3MIgSWpgN0t2UqsjaaEDhmmICKizt-_0iZy8nkEpNnvgqv5bOHDhs7AXlYS1pg8dgPKuyfkhyVIKa3DhuGyb7tFjwJxHpr128BXf1Dbq-p7Njy46tbKsZhP5zGTjdXlqlAhR4Bl5Fxaxr7D0gdTVBVTlUp9DCy6l-pTBpsvHxShkjXJ0GHVpIZdB-c2e_K9PfTW5MDPcHekG9djnWPSEy-fRvKzTsyVFhdy-X3NXQWWkjFv9bNarV-bhxMlzqhujuaeXJGEqUZlkhBxTsqFr1N7XVcmhs3ECdjEyun2fUSge4BoC7budsQ
```

2. Accessing a Protected Resource

Use the generated token to access the protected endpoint:

```bash
export TOKEN=$(curl -s -X POST -u "user:password" http://localhost:8081/token)
curl -H "Authorization: Bearer $TOKEN" http://localhost:8081/
```

You should see a response like:

```bash
Hello, user!
```

## Testing

The project includes both integration and unit tests using MockMvc and @WebMvcTest to verify:

Generation of JWT tokens via the /token endpoint.

Access to the protected resource with a valid token.

Handling of requests without authentication, resulting in a 401 Unauthorized status.
