## Summary:

What is Kong?
- Is an open source API Gateway (Middleware)

What is Konga?
- Opensource admin UI for Kong

What is a service?
- Like a set of configurations: where to route to, which middleware(plugin) to execute.

What is a route?
- Like an input route and service is an output

What a plugin?
- Middle where to execute between each request

What is a consumer?
- Who use the API, what they do

## 0. Run docker compose

```
docker compose up -d
```
## 1. Create a service

```cmd
curl --location --request POST 'http://localhost:8001/services/' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "admin-api",
    "host": "localhost",
    "port": 8001
}'
```

## 2. Create a route

```cmd
curl --location --request POST 'http://localhost:8001/services/{service_id|service_name}/routes' \
--header 'Content-Type: application/json' \
--data-raw '{
    "paths": ["/admin-api"]
}'
```

## 3. Add a auth plugin

```cmd
curl -X POST http://localhost:8001/services/{service_id|service_name}/plugins \
    --data "name=key-auth" 
```

## 4. Add Konga as a consumer

```cmd
curl --location --request POST 'http://localhost:8001/consumers/' \
--form 'username=konga' \
--form 'custom_id=cebd360d-3de6-4f8f-81b2-31575fe9846a'
```

## 5. Create a token 

```cmd
curl --location --request POST 'http://localhost:8001/consumers/e7b420e2-f200-40d0-9d1a-a0df359da56e/key-auth'
```
