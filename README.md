# jwt-gin

The project is a demo that will help you understand how to use JWT to achieve features like registration and login. It uses Gin and Gorm as the frameworks, and uses Golang-Jwt as authentication library. Additionally, it uses MySQL to store the user information, and I hope this is helpful to your project.

## Step 1
Before you start the project, please make sure that you have installed Go and created a database called 'jwt-gin,' as the project uses MySQL to store user information, as mentioned before.

## Step 2
Install the important libraries:
 ```
go get -u github.com/gin-gonic/gin
go get -u github.com/jinzhu/gorm
go get -u github.com/golang-jwt/jwt/v5
go get -u github.com/joho/godotenv
go get -u golang.org/x/crypto

 ```

## Step 3
Update the env file of the project.
```
DB_HOST=localhost                  
DB_DRIVER=mysql              
DB_USER=dev
DB_PASSWORD=123456
DB_NAME=jwt-gin
DB_PORT=3306
```

## Step 4
Start the serve.
```
go run main.go
```

If You can see the output below, it means that the serve is listening on the port 8080.
```
We are connected to the database  mysql
[GIN-debug] [WARNING] Creating an Engine instance with the Logger and Recovery middleware already attached.

[GIN-debug] [WARNING] Running in "debug" mode. Switch to "release" mode in production.
 - using env:   export GIN_MODE=release
 - using code:  gin.SetMode(gin.ReleaseMode)

[GIN-debug] POST   /auth/register            --> jwt-gin/controllers.Register (3 handlers)
[GIN-debug] POST   /auth/login               --> jwt-gin/controllers.Login (3 handlers)
[GIN-debug] GET    /api/user                 --> jwt-gin/controllers.GetUser (4 handlers)
[GIN-debug] [WARNING] You trusted all proxies, this is NOT safe. We recommend you to set a value.
Please check https://pkg.go.dev/github.com/gin-gonic/gin#readme-don-t-trust-all-proxies for details.
[GIN-debug] Listening and serving HTTP on :8080
```

## Step 5 

The process has registered three routers: /auth/register, /auth/login, and /api/user.

If you broswe the /api/user without logging in, it will return you an unauthorized result.

```
{
    "code": 400,
    "msg": "Unauthorized",
    "data": null
}
```

You can post to the /auth/register router to create an account, and use the account to log in by posting to /auth/login.


Post to the /auth/register and pass the parameters below
```
{"username": "helloworld3", "password": "123456"}
```
The process will return the result below if it runs successfully. 
```
{
    "code": 200,
    "msg": "success",
    "data": null
}
```

Post to the /auth/login router and pass the account that you created just before as parameters to log in.
```
{"username": "helloworld3", "password": "123456"}
```
The process will return the token below if it runs successfully.
```
{
    "code": 200,
    "msg": "success",
    "data": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyX2lkIjoxLCJpc3MiOiJqd3QiLCJleHAiOjE3NTI2NDkyMzJ9.KzzMEc-vZW3YAlXM69eftCNEXN_gzxIDXjmJULNR-co"
}
```
Now, you can set the token as the `Authorization` property in the request header and get the user information.

