## Auth Controller

### Base URL
http://localhost:8080/api

------------------------------------------------------------------------------------------------------------------------------------------------------

#### Admin Authentication(Login)
**URL:** `/login`
------------------------------------------------------------------------------------------------------------------------------------------------------
<details>
<summary><code>POST</code> <code><b>/</b></code> <code>(overwrites all in-memory stub and/or proxy-config)</code></summary>

##### Parameters
> | name      |  type     | data type               | description                                                           |
> |-----------|-----------|-------------------------|-----------------------------------------------------------------------|
> | emailId   |  String   | object (JSON )          |Use Authorised admin EmailId for login                                 |
> | password  |  String   | object (JSON )          |Password for authenication                                             |


##### Responses

> | http code     | content-type                      | response                                                            |
> |---------------|-----------------------------------|---------------------------------------------------------------------|
> | `201`         | `text/plain;charset=UTF-8`        | 'http Status: Ok', 'message: Login successful'                      |
> | `401`         | `application/json`                |  'http Status: Bad Request', 'message:Unauthorized operation'       |

##### Example cURL

> ```javascript
>  curl -X POST -H "Content-Type: application/json" --data @post.json http://localhost:8889/
> ```

##### Request Body
    ```json
    {
        "emailId": "user@example.com",
        "password": "userpassword"
    }
    ```
##### Response Body Example
    ```json
    {
        "data": {
            "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c"
        },
        "meta": {
            "message": "Login successful",
            "status": "OK"
        }
    }
    ``` 

</details>

------------------------------------------------------------------------------------------------------------------------------------------------------

#### Renew Token
**URL:** `/renew-token`
------------------------------------------------------------------------------------------------------------------------------------------------------
<details>
 <summary><code>GET</code> <code><b>/</b></code> <code>(gets all in-memory stub & proxy configs)</code></summary>

##### Parameters
>None

##### Description
>Generates a new token for the authorized login to verify and the send the invitation.

##### Responses

> | http code     | content-type                      | response                                                            |
> |---------------|-----------------------------------|---------------------------------------------------------------------|
> | `201`         | `JWT key`                         | 'http Status: Ok', 'message: Token Renewed'                         |
> | `401`         | `application/json`                |  'http Status: Bad Request', 'message:Invalid Token'                |
</details>

------------------------------------------------------------------------------------------------------------------------------------------------------

### Authentication
- **Type:** JWT (JSON Web Token)
- **Authorization Header:** Provide the JWT token obtained during login as a bearer token in the request headers for authenticated endpoints.

### Error Handling
- In case of errors, the API will return appropriate HTTP status codes along with error details in the response body.

### Security
- This API utilizes JWT for authentication, ensuring secure transmission of data over the network.

### Note
- Ensure that proper authentication credentials are provided for accessing secured endpoints.
- Handle authentication tokens securely and avoid exposing them to unauthorized users.


