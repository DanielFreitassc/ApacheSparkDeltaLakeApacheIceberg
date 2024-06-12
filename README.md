# Marketplace api documentação

# BASE URL API PRINCIPAL = http://localhost:8080
# BASE URL MICROSERVICE 1 = http://localhost:8081
# BASE URL MICROSERVICE 2 = http://localhost:8082


Cadastro usuário

POST
```json
http://localhost:8080/auth/register
```
> Body Parameters
```json
{
    "name":"Fulado de Tal",
    "login":"teste@teste.satc.edu.br",
    "password":"Aluno123456789",
    "role":"ADMIN"
}
```
> Response (✅201 Created)
OR
> Response (❌400 Bad request)
---
Login usuário

POST
```json
http://localhost:8080/auth/login
```
> Body Parameters
```json
{
    "login":"teste@teste.satc.edu.br",
    "password":"Aluno123456789"
}
```
> Response (✅200 OK)
```json
{
    "token": "eyJhbGciOi...."
}
```
OR
> Response (❌401 Unauthorized)
```json
{
    "message": "Email ou senha incorreto, Tentativas restantes:  3"
}
```
---

Cadastro de produto

POST
```json
http://localhost:8080/products
```
> Body Parameters
```json
{
    "name":"Milho",
    "price":22,
    "description":"Milho enlatado",
    "validity":"02/02/2023",
    "image":"http://imagem.jpg"
}
```
> Response (✅201 Created)
OR
> Response (❌400 Bad Request)

---
Buscar produtos

GET
```json
http://localhost:8080/products/products?page=0&size=2
```
> Response (✅200)
```json
{
    "totalElements": 3,
    "totalPages": 2,
    "pageable": {
        "pageNumber": 0,
        "pageSize": 2,
        "sort": {
            "sorted": false,
            "empty": true,
            "unsorted": true
        },
        "offset": 0,
        "paged": true,
        "unpaged": false
    },
    "size": 2,
    "content": [
        {
            "id": 1,
            "name": "Soja",
            "price": 12.0,
            "description": "Soja enlatada",
            "validity": "02/02/2023",
            "image":"http://imagem.jpg"
        },
        {
            "id": 2,
            "name": "Milho",
            "price": 22.0,
            "description": "Milho enlatado",
            "validity": "02/02/2023",
            "image":"http://imagem.jpg"
            
        }
    ],
    "number": 0,
    "sort": {
        "sorted": false,
        "empty": true,
        "unsorted": true
    },
    "numberOfElements": 2,
    "first": true,
    "last": false,
    "empty": false
}
```
OR
> Response (❌404 Not Found)
```json
{
    "status": "NOT_FOUND",
    "message": "Nenhum produto cadastrado no momento"
}
```

---
Buscar produto por ID

GET
```json
http://localhost:8080/products/{id}
```
> Response (✅200)
```json
{
    "id": 4,
    "name": "Milho",
    "price": 22.0,
    "description": "Milho enlatado",
    "validity": "02/02/2023",
    "image":"http://imagem.jpg"
}
```
OR
> Response (❌404 Not Found)
```json
{
    "status": "NOT_FOUND",
    "message": "Nenhum produto com este ID"
}
```
---
Atualizar produto por ID

PUT
```json
http://localhost:8080/products/{id}
```
> Body parameters
```json
{
    "name":"Milho",
    "price":22,
    "description":"Milho enlatado",
    "validity":"02/02/2023",
    "image":"http://imagem.jpg"
}
```
> Response (✅200)
```json
{
    "id": 4,
    "name": "Milho",
    "price": 22.0,
    "description": "Milho enlatado",
    "validity": "02/02/2023",
    "image":"http://imagem.jpg"
}
```
OR
> Response (❌404 Not Found)
```json
{
    "status": "NOT_FOUND",
    "message": "Nenhum produto com este ID"
}
```
---
Remove produto por ID
DELETE
```json
http://localhost:8080/products/{id}
```
> Response (✅200)
```json
{
    "id": 2,
    "name": "Milho",
    "price": 22.0,
    "description": "Milho enlatado",
    "validity": "02/02/2023",
    "image":"http://imagem.jpg"
}
```
OR

> Response (❌404 Not Found)
```json
{
    "status": "NOT_FOUND",
    "message": "Nenhum produto com este ID"
}
```

Buscar por desperdicio alimentar
```json
http://localhost:8080/products/waste
```
> Response (✅200)
```json
{
    "foodType": "Milho",
    "quantity": 58,
    "date": "02/06/2024",
    "alertMessage": "Quantidade de disperdicio do produto: Milho é alta. Data: 2024-06-02"
}
```
OR
> Response (❌403 Forbidden)
---
Busca informações nos sensores
```json
http://localhost:8080/sensor
```
> Response (✅200 OK)
```json
{
    "umidade": "84.00%",
    "temperatura": "19.10°C",
    "nivelDeLuzSolar": "874.8",
    "quantidadeDeAduboUsado": "38.90%",
    "umidadeMensagem": "Umidade alta. Reduza a quantidade de água.",
    "temperaturaMensagem": "Temperatura em nível adequado.",
    "nivelDeLuzSolarMensagem": "Nível de luz solar em nível adequado.",
    "quantidadeDeAduboUsadoMensagem": "Pouco adubo utilizado. Adicione mais adubo."
}
```
---
```json
http://localhost:8081/waste
```
> Response (✅200 OK)
```
{
    "foodType": "Milho",
    "quantity": 97,
    "date": "12/06/2024"
}
```
---
```json
http://localhost:8082/sensor-data
```
> Response (✅200 OK)
```
{
    "umidade": "42.3",
    "temperatura": "37.2",
    "nivelDeLuzSolar": "684.0",
    "quantidadeDeAduboUsado": "45.9"
}
```
---
Mostrar integrantes do tabalho e tema
```json
http://localhost:8080/ajuda
```

> Response (✅200 OK)
```json
{
    "estudantes": [
        "Daniel Freitas",
        "Geanlucca Zappe"
    ],
    "projeto": "Agricultura e Segurança Alimentar",
    "tema": "Marketplace "
}
```


