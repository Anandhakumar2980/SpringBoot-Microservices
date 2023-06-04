# SpringBoot-Microservices
## Key Components of a Microservices Architecture

### Core Services:

Each service is a self-contained unit of functionality that can be developed, tested, and deployed independently of the other services.

### Service registry:

A service registry is a database of all the services in the system, along with their locations and capabilities. It allows services to discover and communicate with each other.

### API Gateway: 

An API gateway is a single entry point for all incoming requests to the microservices. It acts as a reverse proxy, routing requests to the appropriate service and handling tasks such as authentication and rate limiting.

### Message bus:

A message bus is a messaging system that allows services to communicate asynchronously with each other. This can be done through protocols like HTTP, RabbitMQ, or Kafka.

### Monitoring and logging: 

Monitoring and logging are necessary to track the health of the services and troubleshoot problems.

### Service discovery and load balancing: 

This component is responsible for discovering service instances and directing traffic to the appropriate service instances based on load and availability.

### Continuous integration and continuous deployment (CI/CD):

To make the development and deployment process of microservices as smooth as possible, it is recommended to use a tool such as Jenkins, TravisCI, or CircleCI to automate the process of building, testing, and deploying microservices.

# Microservices Communication

####  Synchronous Communication

  -   In the case of Synchronous Communication, the client sends a request and waits for a response from the service. The important point here is that the protocol (HTTP/HTTPS) is synchronous and the client code can only continue its task when it receives the HTTP server response. 

####  Asynchronous Communication

 -  In the case of asynchronous communication, we have to use a message broker for asynchronous communication between multiple microservices.<br>
 -  For example, we can use RabbitMQ or Apache Kafka as a message broker in order to make an asynchronous communication between multiple microservices and each microservice in a microservices project can expose REST APIs.

##  Synchronous Communication
  
      -  RestTemplate
      -  WebClient
      -  Spring Cloud Open Feign library

## Spring Boot Microservices Communication using Rest Template

       -  RestTemplate is a synchronous client for making HTTP requests in Spring Framework. It provides a convenient way to interact with RESTful APIs and        communicate with other microservices or external services.

#### Advantages and uses of RestTemplate include:

- Simplified HTTP Requests: RestTemplate encapsulates the complexity of making HTTP requests, handling connections, managing headers, and processing responses. It provides a high-level API for performing common HTTP operations, such as GET, POST, PUT, DELETE, etc.

- Communication Between Microservices: RestTemplate allows easy communication between microservices in a distributed system. Microservices can make HTTP requests to other microservices' APIs using RestTemplate, enabling them to exchange data and collaborate seamlessly.

- Integration with Third-Party APIs: RestTemplate can be used to integrate with external APIs, such as payment gateways, social media platforms, weather services, etc. It simplifies the process of sending requests, handling responses, and extracting data from the external services.

- Customizable and Extensible: RestTemplate provides various methods and options for customization. You can set request headers, handle response status codes, configure timeouts, and customize error handling. It also supports pluggable message converters, allowing you to work with different data formats, such as JSON, XML, etc.

- Interceptors and Filters: RestTemplate allows you to add interceptors and filters to modify or inspect the outgoing requests and incoming responses. Interceptors can be useful for tasks like logging, request/response modification, authentication, and more.

- Widely Used in Spring Ecosystem: RestTemplate is a core component of the Spring Framework and is widely adopted in Spring-based applications. It integrates seamlessly with other Spring features, such as dependency injection, exception handling, and declarative transaction management.

- Legacy System Integration: RestTemplate can be used to integrate with legacy systems that expose RESTful APIs. It provides a convenient way to consume and process data from such systems, enabling smooth integration with modern microservice architectures.

![image](https://github.com/Anandhakumar2980/SpringBoot-Microservices/assets/126327213/e3fa205c-b610-41ee-ac06-7599e2b1b22b)

#### Step 1 : Add Spring WebFlux Dependency

```
                        <dependency>
                              <groupId>org.springframework.boot</groupId>
                              <artifactId>spring-boot-starter-web</artifactId>
                        </dependency>
```

#### Step 2: Configure RestTemplate as Spring Bean

```
@SpringBootApplication
public class UserServiceApplication {

    public static void main(String[] args) {
        SpringApplication.run(UserServiceApplication.class, args);
    }

    @Bean
    public RestTemplate restTemplate(){
        return new RestTemplate();
    }
}
```

#### Step 3: Inject and Use RestTemplate to Call the REST API

```
           ResponseEntity<DepartmentDto> responseEntity = restTemplate
                .getForEntity("http://localhost:8080/api/departments/" + user.getDepartmentId(),
                DepartmentDto.class);

```


## Spring Boot Microservices Communication using WebClient

- WebClient is a non-blocking, reactive client to perform HTTP requests, exposing a fluent, reactive API over underlying HTTP client libraries such as Reactor Netty.

- To use WebClient in our Spring boot project, we have to add Spring WebFlux dependency to the classpath.
WebClient is a non-blocking, reactive client for making HTTP requests in Spring Framework. It is the recommended replacement for the synchronous RestTemplate in Spring 5 and is particularly well-suited for reactive and asynchronous applications.

#### Advantages and uses of WebClient include:

- Non-Blocking and Reactive: WebClient is built on the reactive programming model, which enables non-blocking and asynchronous communication. It leverages the power of reactive streams and allows you to handle a large number of concurrent requests with a smaller number of threads, leading to better resource utilization and scalability.

- Performance and Efficiency: Due to its non-blocking nature, WebClient can achieve better performance compared to traditional blocking clients like RestTemplate. It can efficiently handle high loads and concurrent requests without blocking threads, leading to improved application responsiveness and throughput.

- Flexibility and Composition: WebClient provides a flexible and functional API for building and composing HTTP requests. It offers a fluent and declarative approach to constructing requests, applying filters, setting headers, handling responses, and extracting data. It allows you to compose complex request pipelines and apply reusable request/response transformations.

- Streaming and Chunked Responses: WebClient supports streaming and chunked responses, which are useful when dealing with large or continuous data streams. It can handle and process the data incrementally as it arrives, which is beneficial for scenarios like real-time updates, event-driven architectures, and processing large files.

- Built-in Reactor Core Integration: WebClient seamlessly integrates with Reactor Core, the reactive library used in Spring WebFlux. It can easily convert responses to reactive types, such as Mono and Flux, allowing you to leverage reactive operators for composing and processing data streams.

- Integration with Spring WebFlux: WebClient is the preferred choice for making HTTP requests in Spring WebFlux applications. It aligns well with the reactive programming model and is fully compatible with other reactive components in the Spring ecosystem, such as WebFlux, WebFlux WebClient, and Spring Data Reactive.

- API Testing and Mocking: WebClient can be used for testing APIs and writing integration tests. It provides a convenient way to send requests and verify responses in a test environment. Additionally, it integrates well with tools like WebTestClient to simplify the testing of Spring WebFlux applications.

![image](https://github.com/Anandhakumar2980/SpringBoot-Microservices/assets/126327213/bb259756-e805-4eb9-9a59-4f617fe699ac)

#### Step 1 : Add Spring WebFlux Dependency

                            <dependency>
		                     	<groupId>org.springframework.boot</groupId>
		                     	<artifactId>spring-boot-starter-webflux</artifactId>
		                  </dependency>

#### Step 2: Configure WebClient as Spring Bean

```
@SpringBootApplication
public class UserServiceApplication {

    public static void main(String[] args) {
        SpringApplication.run(UserServiceApplication.class, args);
    }

    @Bean
    public WebClient webClient(){
        return WebClient.builder().build();
    }
}
```
#### Step 3: Inject and Use WebClient to Call the REST API

```
        DepartmentDto departmentDto = webClient.get()
                 .uri("http://localhost:8080/api/departments/" + user.getDepartmentId())
                         .retrieve()
                                 .bodyToMono(DepartmentDto.class)
                                         .block();

```


## Spring Boot Microservices Communication using Spring Cloud Open Feign

- WebClient is a non-blocking, reactive client to perform HTTP requests, exposing a fluent, reactive API over underlying HTTP client libraries such as Reactor Netty.

-  Spring Cloud Open Feign is a declarative web service client that simplifies communication between microservices in a Spring Boot application. It builds on top of the Spring Cloud ecosystem and provides a higher-level abstraction for making HTTP requests.

- To use WebClient in our Spring boot project, we have to add Spring WebFlux dependency to the classpath.
WebClient is a non-blocking, reactive client for making HTTP requests in Spring Framework. It is the recommended replacement for the synchronous RestTemplate in Spring 5 and is particularly well-suited for reactive and asynchronous applications.

#### Advantages and uses of Spring Cloud Open Feign include:

- Declarative Programming Model: Spring Cloud Open Feign allows you to define the web service clients using a declarative programming model. By using annotations and interfaces, you can easily define the API contracts and mappings without writing low-level HTTP client code.

- Integration with Service Discovery: Spring Cloud Open Feign integrates seamlessly with service discovery mechanisms provided by Spring Cloud, such as Netflix Eureka or Spring Cloud Consul. It enables automatic service registration and discovery, allowing microservices to locate and communicate with each other without hardcoding URLs.

- Load Balancing and Resilience: Spring Cloud Open Feign supports client-side load balancing and resilience patterns out of the box. It integrates with Spring Cloud LoadBalancer to distribute requests across multiple instances of a service. It also provides circuit breaker functionality using tools like Hystrix or resilience4j to handle failures and fallback mechanisms.

- Error Handling and Exception Propagation: With Spring Cloud Open Feign, you can define custom error handling strategies for different types of exceptions. It provides mechanisms to propagate exceptions from the server-side to the client-side, making it easier to handle and process error responses in a consistent manner.

- Request/Response Interceptors: Spring Cloud Open Feign allows you to define request and response interceptors to modify or inspect HTTP requests and responses. Interceptors can be used for various purposes, such as logging, adding authentication headers, or modifying request/response data.

- Integration with Spring Boot Actuator: Spring Cloud Open Feign integrates seamlessly with Spring Boot Actuator, providing detailed metrics, monitoring, and tracing capabilities. You can easily monitor the performance and health of your Feign clients using Actuator endpoints and integrate with tools like Prometheus or Zipkin.

- Integration with Spring Cloud Gateway: Spring Cloud Open Feign can be combined with Spring Cloud Gateway to create a powerful API gateway solution. The combination of Feign and Gateway allows you to centralize the routing, filtering, and security of microservices APIs, providing a single entry point for clients.

- Integration Testing: Spring Cloud Open Feign provides support for integration testing, allowing you to test the interactions between microservices in an automated manner. You can use tools like Spring Cloud Contract to define and verify contracts between Feign clients and the server-side services.

![image](https://github.com/Anandhakumar2980/SpringBoot-Microservices/assets/126327213/a54f40c0-c58d-4564-8e16-a29607bde2f7)

#### Step 1 : Add Spring WebFlux Dependency

```
                        <dependency>
		                      	<groupId>org.springframework.cloud</groupId>
		                      	<artifactId>spring-cloud-starter-openfeign</artifactId>
	                     	</dependency>
```

#### Step 2: Configure WebClient as Spring Bean

```
@SpringBootApplication
@EnableFeignClients   -- main annotation
public class UserServiceApplication {

    public static void main(String[] args) {
        SpringApplication.run(UserServiceApplication.class, args);
    }
}
```
#### Step 3: Inject and Use WebClient to Call the REST API

```
@FeignClient(value = "DEPARTMENT-SERVICE", url = "http://localhost:8080")
public interface APIClient {
    @GetMapping(value = "/api/departments/{id}")
    DepartmentDto getDepartmentById(@PathVariable("id") Long departmentId);
}
```













