## Authorization

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

------------------------------------------------------------------------------------------------------------------------------------------------------

## Invitation

### Base URL
http://localhost:8080/api/invite

------------------------------------------------------------------------------------------------------------------------------------------------------

#### New Invitation
**URL:** `/new`
------------------------------------------------------------------------------------------------------------------------------------------------------
<details>
<summary><code>POST</code> <code><b>/</b></code> <code>(overwrites all in-memory stub and/or proxy-config)</code></summary>

#### Parameters
> | name      |  type     | data type               | description                                                           |
> |-----------|-----------|-------------------------|-----------------------------------------------------------------------|
> | userName  |  String   | object (JSON )          |Invitee Name                                                           |
> | emailId   |  String   | object (JSON )          |Invitee emailId                                                        |
> | role      |  String   | object (JSON )          |role of the invitee(Admin, Coaches, mentors, ventures, mentees)        |

#### Respones
> | http code     | content-type                      | response                                                            |
> |---------------|-----------------------------------|---------------------------------------------------------------------|
> | `201`         | `text/plain;charset=UTF-8`        | 'http Status: Ok', 'message: Invitation sent successfully'          |
> | `401`         | `application/json`                |  'http Status: Bad Request', 'message:Invitation already sent'      |
> | `401`         | `application/json`                |  'http Status: Bad Request', 'message:User Exists'                  |
> | `401`         | `application/json`                |  'http Status: Bad Request', 'message:Invitation to Same Role'      |
> | `401`         | `application/json`                |  'http Status: Bad Request', 'message:Invitation to Invalid Role'   |
> | `500`         | `application/json`                |  'http Status: Bad request', 'message:Internal Server error'        |

#### Example cURL
>```javascript
>curl -X POST \
>https://your-api-domain.com/invite/new \
>-H 'Content-Type: application/json' \
>-d '{
>       "email": "user@example.com",
>       "role": "ROLE_USER"
>   }'
>```

#### Request Body
>```json
>{
>   "name":"user_name",
>   "email": "user@example.com",
>   "role": "ROLE_USER"
>}
>```

#### Response Body
>```json
>{
>   "message": "Invitation created successfully"
>}
>```
</details>

------------------------------------------------------------------------------------------------------------------------------------------------------

#### Resend Invitation
**URL:**  `/resend`
------------------------------------------------------------------------------------------------------------------------------------------------------
<details>
<summary><code>POST</code> <code><b>/</b></code> <code>(overwrites all in-memory stub and/or proxy-config)</code></summary>

#### Parameters
> | name      |  type     | data type               | description                                                           |
> |-----------|-----------|-------------------------|-----------------------------------------------------------------------|
> | invId     |  UUID     | object (JSON )          |Invitation Id                                                          |

#### Responses
> | http code     | content-type                      | response                                                            |
> |---------------|-----------------------------------|---------------------------------------------------------------------|
> | `401`         | `application/json`                | 'http Status: Bad Request', 'message: Invalid Invitation'           |
> | `401`         | `application/json`                |  'http Status: Bad Request', 'message:Invitation Already Accepted'  |
> | `401`         | `application/json`                |  'http Status: Bad Request', 'message:Unauthorized Operation'       |

#### Example cURL
>```javascript
>curl -X POST \  'https://your-api-domain.com/invite/resend?invId=invitation_id_here' \
>-H 'Authorization: Bearer <your_access_token>'
>```

------------------------------------------------------------------------------------------------------------------------------------------------------

#### Verify Invitation
**URL:** `/verifyInvite`
------------------------------------------------------------------------------------------------------------------------------------------------------
<details>
 <summary><code>GET</code> <code><b>/</b></code> <code>(gets all in-memory stub & proxy configs)</code></summary>

#### Parameters
> | name      |  type     | data type               | description                                                           |
> |-----------|-----------|-------------------------|-----------------------------------------------------------------------|
> | token     |  UUID     | object (JSON )          |Invitation Token (used to verify the invitation)                       |

#### Responses
> | http code     | content-type                      | response                                                            |
> |---------------|-----------------------------------|---------------------------------------------------------------------|
> | `401`         | `application/json`                | 'http Status: Bad Request', 'message: Invalid Invitation Token'     |
> | `401`         | `application/json`                |  'http Status: Bad Request', 'message:Invitation Already Accepted'  |
> | `401`         | `application/json`                |  'http Status: Bad Request', 'message:Invitation expired'           |

#### Example cURL
>```javascript
>curl -X GET \
> 'https://your-api-domain.com/invite/verifyInvite?token=invitation_token_here'
>```

#### Response Body Example
>```json
>{
>   "data": {
>       "id": "invitation_id",
>       "email": "user@example.com",
>       "role": "ROLE_USER"
>   }
>}
>```
</details>

------------------------------------------------------------------------------------------------------------------------------------------------------

#### Accept Invitation and Create User
**URL:** `/acceptInvitation`
------------------------------------------------------------------------------------------------------------------------------------------------------
<details>
<summary><code>POST</code> <code><b>/</b></code> <code>(overwrites all in-memory stub and/or proxy-config)</code></summary>

#### Parameters
> | name      |  type     | data type               | description                                                           |
> |-----------|-----------|-------------------------|-----------------------------------------------------------------------|
> | token     |  UUID     | object (JSON )          |Invitation Token (used to verify the invitation)                       |
> | userName  |  String   | object (JSON )          |User Name                                                              |
> | emailId   |  String   | object (JSON )          |Use Authorised EmailId for login                                       |
> | password  |  String   | object (JSON )          |Password for authenication                                             |
> | contact   |  String   | object (JSON )          |User contact                                                           |
> | Linkedin  |  String   | object (JSON )          |Social Media                                                           |
> | Role      |  String   | object (JSON )          |Role provided by the admin                                             |

#### Responses
> | http code     | content-type                      | response                                                            |
> |---------------|-----------------------------------|---------------------------------------------------------------------|
> | `201`         | `text/plain;charset=UTF-8`        | 'http Status: Ok', 'message: User created successfully'             |
> | `201`         | `text/plain;charset=UTF-8`        | 'http Status: Ok', 'message: Invitation Accepted'                   |
> | `401`         | `application/json`                |  'http Status: Bad Request', 'message:Invalid Invitation '          |
> | `401`         | `application/json`                |  'http Status: Bad Request', 'message:Invitation Expired'           |
> | `500`         | `application/json`                |  'http Status: Internal Server Error', 'message:Error occured while processing the request'        |

#### Example cURL
>```javascript
>curl -X POST \
>'https://your-api-domain.com/invite/acceptInvitation?token=invitation_token_here' \
> -H 'Content-Type: application/json' \
> -d '{
>       "username": "newuser",
>       "password": "password"
>   }'
>```
</details>

------------------------------------------------------------------------------------------------------------------------------------------------------


