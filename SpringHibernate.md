
The primary propagation types are:

    REQUIRED (Default):
    This is the most common type. If a transaction is already in progress, the method joins that existing transaction. If no transaction exists, a new one is created.
    REQUIRES_NEW:
    A new, independent transaction is always started for the method. If an existing transaction is active, it is suspended until the new transaction completes.
    SUPPORTS:
    If a transaction exists, the method participates in it. If no transaction is active, the method executes non-transactionally.
    NOT_SUPPORTED:
    The method always executes non-transactionally. If a transaction is currently active, it is suspended for the duration of the method's execution.
    MANDATORY:
    The method requires an existing transaction. If no transaction is active when the method is called, an exception is thrown.
    NEVER:
    The method must never execute within a transaction. If a transaction is active when the method is called, an exception is thrown.
    NESTED:
    If a transaction exists, a nested transaction (using savepoints) is created within it. This allows the nested transaction to roll back independently without affecting the outer transaction, while still being part of the same overall transaction if the outer transaction rolls back. Note that not all JPA providers support nested transactions. 


Spring Framework allows developers to control the isolation level of transactions, which dictates how concurrent transactions interact with each other and the degree to which they are isolated. This is crucial for maintaining data consistency and preventing concurrency issues like dirty reads, non-repeatable reads, and phantom reads.
Spring supports the following transaction isolation levels, primarily through the isolation attribute of the @Transactional annotation:

    Isolation.DEFAULT:
    This uses the default isolation level configured for the underlying database. The specific default level varies depending on the database system (e.g., PostgreSQL defaults to READ_COMMITTED).

Isolation.READ_UNCOMMITTED:
This is the lowest isolation level. Transactions can read uncommitted changes made by other concurrent transactions, leading to "dirty reads." It offers high concurrency but the lowest data integrity. 
Isolation.READ_COMMITTED:
This level prevents dirty reads by ensuring that a transaction only reads data that has been committed by other transactions. However, it still allows "non-repeatable reads" (a row read twice within the same transaction can have different values if another transaction commits a change between the reads) and "phantom reads" (new rows appearing in a result set if another transaction inserts rows matching the query criteria).
Isolation.REPEATABLE_READ:
This level prevents both dirty reads and non-repeatable reads. Once a transaction reads a row, subsequent reads of that same row within the same transaction will return the same value, even if another transaction commits changes to that row. However, it may still allow phantom reads.
Isolation.SERIALIZABLE:
This is the highest and most restrictive isolation level. It ensures full isolation from other transactions, preventing dirty reads, non-repeatable reads, and phantom reads. It achieves this by effectively serializing transactions, meaning they appear to execute one after another, which can significantly reduce concurrency. 

Feign Client in Spring Boot
@FeignClient(name="servicename",url="${url}")
public interface InternalService{
	@getrequest(@urlParam/@pathparam)
	List<Bean> getData(name){
	}
}

https://www.youtube.com/watch?v=wmawYODmQU0&t=99s
https://www.youtube.com/watch?v=B8x4wBBT6M0
https://www.youtube.com/watch?v=8Ooxz2dgtPo
https://www.youtube.com/watch?v=7nm1pYuKAhY

https://www.youtube.com/watch?v=sSKhdZ32YpY


## exception Handling
*   We can use @ExceptionHandler anotation and write method.any ArithmeticException throw in that class will go to this method and throw message
  @ExceptionHandler(ArithmeticException.class)
  public String handleArithmeticException(ArithmeticException ex) {
        return "Error: Cannot divide by zero!";
    }
*   Advices like ControllerAdvice or RestControlerAdvice are grobale advices.That will call expections from global
  @RestControllerAdvice
  public class AppExceptionHandler {

    @ExceptionHandler(UserNotFoundException.class)
    public ResponseEntity<String> handleUserNotFound(UserNotFoundException ex) {
        return new ResponseEntity<>(ex.getMessage(), HttpStatus.NOT_FOUND);
    }
}
* we can achive using AOP for custom expections
## Authenication and autherizatio@Configuration 
  @Configuration or @EnableWebSecurity,@EnableMethodSecurity
public class SecurityConfig {

    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http
            .csrf(csrf -> csrf.disable())
            .authorizeHttpRequests(auth -> auth
                .requestMatchers("/api/auth/**").permitAll()
                .anyRequest().authenticated()
            )
            .oauth2ResourceServer(oauth2 -> oauth2.jwt()); // configure JWT validation if needed

        return http.build();
    }
}
           +----------------------+
           |   @EnableWebSecurity |
           +----------------------+
                     |
                     v
        +--------------------------+
        | SecurityFilterChain Bean |
        +--------------------------+
                     |
                     v
          +--------------------+
          | HttpSecurity config|
          +--------------------+
          |  - Endpoint rules  |
          |  - CSRF / CORS     |
          |  - Authentication  |
          |  - Authorization   |
          +--------------------+
                     |
                     v
        +--------------------------+
        | Spring Security Filters  |
        |  (Filter Chain)          |
        +--------------------------+
                     |
                     v
          +--------------------+
          | Incoming HTTP Req  |
          +--------------------+
                     |
                     v
     +-----------------------------+
     | AuthenticationManager       |
     |  - Validates credentials    |
     |  - Checks JWT, DB, etc.    |
     +-----------------------------+
                     |
          +----------------------+
          | AuthorizationManager |
          |  - Checks roles/perm |
          +----------------------+
                     |
                     v
          +--------------------+
          |   Controller /     |
          |   Endpoint logic   |
          +--------------------+

