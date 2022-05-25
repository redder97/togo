### Requirements

- Implement one single API which accepts a todo task and records it
  - There is a maximum **limit of N tasks per user** that can be added **per day**.
  - Different users can have **different** maximum daily limit.
- Write integration (functional) tests
- Write unit tests
- Choose a suitable architecture to make your code simple, organizable, and maintainable
- Write a concise README
  - How to run your code locally?
  - A sample “curl” command to call your API
  - How to run your unit tests locally?
  - What do you love about your solution?
  - What else do you want us to know about however you do not have enough time to complete?

## README PROPER

### Requirements
 * [Jdk 11+](https://www.oracle.com/ph/java/technologies/javase/jdk11-archive-downloads.html)
 * [Maven 3.8.5](https://maven.apache.org/download.cgi)
 * [Postgres Server 11+](https://www.postgresql.org/download/)

### Environment Setup
1) Ensure that the specified versions of requirements are installed.
2) Ensure postgres server connectivity
LinuxOS/MacOS:
> `psql -h localhost -U $psql_user`
3) create database
> `CREATE DATABASE todo_test`

### Running the server locally
1) navigate into project's root 
> `cd $projectDir\`
2) install dependencies 
> `mvn clean install` 
3) Run the project
> `mvn spring-boot:run`

### Sample cURL command for testing
> `curl --location --request GET 'http://localhost:8008/api/v1/version'`

#### Sequenced Tests using cURL
- create a user
  > `curl --location --request POST 'http://localhost:8008/api/v1/users/create' \
  --header 'Content-Type: application/json' \
  --data-raw '{
  "username" : "user123x",
  "password" : "pass123",
  "todoLimit" : 3
  }'`
- login 
  > `curl --location --request POST 'http://localhost:8008/api/v1/users/login' \
 --header 'Content-Type: application/json' \
 --data-raw '{
 "username" : "user123x",
 "password" : "pass123"
 }'`
- copy *$token* from `message` property of the response body. (This will serve as auth/jwt)
- create a task
  > `curl --location --request GET 'http://localhost:8008/api/v1/todos/create' \
 --header 'Authorization: Bearer $token' \
 --header 'Content-Type: application/json' \
 --data-raw '{
 "task": "ask for money again"
 }
 '`
- list all tasks
  > `curl --location --request GET 'http://localhost:8008/api/v1/todos/list?page=0&size=3' \
 --header 'Authorization: Bearer $token'`

 
### Running Tests
1) navigate into project's root
> `cd $projectDir\`
2) run test command
> `mvn clean test`

### Troubleshooting | FAQ
1) Changing datasource
* To change the datasource, navigate to `src/main/resources/application.properties` 
and modify `spring.datasource.*` properties as needed
2) Change deployment port
* To change the deployment port, navigate to `src/main/resources/application.properties`
and modify `server.port`
