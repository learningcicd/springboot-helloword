# Hello World Spring Boot Application

A simple "Hello World" web application built with Spring Boot and Java 8.

## Overview

This is a basic Spring Boot REST API application that demonstrates fundamental concepts including:
- Spring Boot application setup
- REST controller endpoints
- Path variables and query parameters
- Maven dependency management

## Prerequisites

Before running this application, ensure you have the following installed:
- **Java 8** (JDK 1.8 or higher)
- **Maven 3.6+**
- **Git** (optional, for cloning)

## Project Structure

```
hello-world/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/example/helloworld/
│   │   │       ├── HelloWorldApplication.java
│   │   │       └── controller/
│   │   │           └── HelloWorldController.java
│   │   └── resources/
│   └── test/
├── pom.xml
└── README.md
```

### POM (pom.xml)
```bash
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
         http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>hello-world</artifactId>
    <version>1.0.0</version>
    <packaging>jar</packaging>

    <name>Hello World Spring Boot</name>
    <description>A simple Hello World Spring Boot application</description>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.7.18</version>
        <relativePath/>
    </parent>

    <properties>
        <java.version>1.8</java.version>
        <maven.compiler.source>1.8</maven.compiler.source>
        <maven.compiler.target>1.8</maven.compiler.target>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
</project>
```

### App Code
```bash
package com.example.helloworld;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class HelloWorldApplication {

    public static void main(String[] args) {
        SpringApplication.run(HelloWorldApplication.class, args);
    }
}
```
## App Controller

```bash
package com.example.helloworld.controller;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloWorldController {

    @GetMapping("/")
    public String home() {
        return "Hello World! Welcome to Spring Boot!";
    }

    @GetMapping("/hello")
    public String hello() {
        return "Hello World from Spring Boot!";
    }

    @GetMapping("/hello/{name}")
    public String helloWithName(@PathVariable String name) {
        return "Hello, " + name + "! Welcome to Spring Boot!";
    }

    @GetMapping("/greet")
    public String greet(@RequestParam(value = "name", defaultValue = "World") String name) {
        return "Hello, " + name + "!";
    }
}
```

### Properties

```bash
# Change server port
server.port=9090

# Change context path
server.servlet.context-path=/api

# Set logging level
logging.level.com.example.helloworld=DEBUG
```

## Getting Started

### 1. Clone or Download

Clone this repository or download the source code to your local machine.

### 2. Build the Application

Navigate to the project directory and run:

```bash
mvn clean compile
```

### 3. Run the Application

You can run the application using Maven:

```bash
mvn spring-boot:run
```

Alternatively, you can build a JAR file and run it:

```bash
mvn clean package
java -jar target/hello-world-1.0.0.jar
```

### 4. Access the Application

Once the application starts, you'll see output similar to:
```
Started HelloWorldApplication in X.XXX seconds
```

The application will be available at: `http://localhost:8080`

## API Endpoints

The application provides the following REST endpoints:

| Method | Endpoint | Description | Example |
|--------|----------|-------------|---------|
| GET | `/` | Basic welcome message | `curl http://localhost:8080/` |
| GET | `/hello` | Simple hello endpoint | `curl http://localhost:8080/hello` |
| GET | `/hello/{name}` | Personalized greeting with path variable | `curl http://localhost:8080/hello/John` |
| GET | `/greet` | Greeting with optional query parameter | `curl http://localhost:8080/greet?name=Alice` |

### Example Responses

```bash
# GET /
Hello World! Welcome to Spring Boot!

# GET /hello
Hello World from Spring Boot!

# GET /hello/John
Hello, John! Welcome to Spring Boot!

# GET /greet?name=Alice
Hello, Alice!

# GET /greet (without parameter)
Hello, World!
```

## Testing the Application

### Using curl

```bash
# Test basic endpoint
curl http://localhost:8080/

# Test with path variable
curl http://localhost:8080/hello/YourName

# Test with query parameter
curl http://localhost:8080/greet?name=YourName
```

### Using a Web Browser

Simply open your browser and navigate to:
- http://localhost:8080/
- http://localhost:8080/hello
- http://localhost:8080/hello/YourName
- http://localhost:8080/greet?name=YourName

## Configuration

### Default Configuration

The application runs with Spring Boot's default configuration:
- **Port**: 8080
- **Context Path**: /
- **Logging Level**: INFO

### Custom Configuration

To modify the default settings, create an `application.properties` file in `src/main/resources/`:

```properties
# Change server port
server.port=9090

# Change context path
server.servlet.context-path=/api

# Set logging level
logging.level.com.example.helloworld=DEBUG
```

## Dependencies

This project uses the following key dependencies:

- **Spring Boot Starter Web** (2.7.18) - For web application and REST API functionality
- **Spring Boot Starter Test** - For testing capabilities
- **Java 8** compatibility

## Building for Production

To create a production-ready JAR file:

```bash
mvn clean package -DskipTests
```

The JAR file will be created in the `target/` directory and can be deployed to any environment with Java 8+.

## Troubleshooting

### Common Issues

**Port already in use**: If port 8080 is occupied, either:
- Stop the process using port 8080
- Change the port in `application.properties`: `server.port=8081`

**Java version**: Ensure you're using Java 8 or higher:
```bash
java -version
```

**Maven issues**: Verify Maven installation:
```bash
mvn --version
```

## Next Steps

This basic application can be extended with:
- Database integration (JPA/Hibernate)
- Security (Spring Security)
- Additional REST endpoints
- Front-end integration
- Unit and integration tests
- Docker containerization

## License

This project is open source and available under the MIT License.
