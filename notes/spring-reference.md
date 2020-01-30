# Spring Reference

A list of annotations, classes, and files used in class.

## Bootstrapping

* [Using the @SpringBootApplication Annotation](https://docs.spring.io/spring-boot/docs/current/reference/html/using-spring-boot.html#using-boot-using-springbootapplication-annotation)

`@SpringBootApplication`  
Annotates the class containing your program's main method. Initializes various
default settings.

`SpringApplication`  
Class with helper methods to launch your application. Used in your application's
main method.

## Dependency Injection

Features for configuration, class dependencies, and code reuse.

* [Java-based Container Configuration](https://docs.spring.io/spring/docs/current/spring-framework-reference/core.html#beans-java)
* [Annotation-based Container Configuration](https://docs.spring.io/spring/docs/current/spring-framework-reference/core.html#beans-annotation-config)

`ApplicationContext`  
A big "tool bag" holding many "tools" (classes configured by Spring and you
application).

`@Component`  
Annotates a class for reuse throughout the application. Adds your class to the
tool bag.

`@Autowired`  
Annotates a field indicating that class should be fetched from the
ApplicationContext. It marks the location where you want to use a tool from the
tool bag.

`application.properties`  
A file containing name/value pairs that configure the application. You can add
your own name/value pairs here to further customize your application

`@Value`  
Inject a value from `application.properties` into a property in one of your
classes.

## Web

Features for handling web requests and returning responses.

* [Web Documentation](https://docs.spring.io/spring/docs/current/spring-framework-reference/web.html)
* [Validator Interface](https://docs.spring.io/spring/docs/current/spring-framework-reference/core.html#validator)
* [Validation Using JSR-303 Annotations](https://docs.spring.io/spring/docs/current/spring-framework-reference/core.html#validation-beanvalidation-overview)

`@Controller`, `@RestController`  
Annotate classes that handle web requests.

`@RequestMapping`  
Annotates a method, describing which requests it should handle. By default,
this annotation will map **ALL** HTTP methods to the Java method it annotates.
Be careful if this is not the behavior you expect.

`@GetMapping`, `@PostMapping`, `@DeleteMapping`, etc.  
Like `@RequestMapping`, but only map requests for a specific HTTP method. Prefer one of these annotations over `@RequestMapping` for their specificity.

`@RequestParameter`  
Maps a request parameter to a method argument. By default, the name of the
method argument is expected to match the name of the request parameter.

`@PathVariable`  
Used in conjunction with `@RequestMapping` and its derivatives. Maps a portion
of the path to method argument.

`@ResponseBody`  
When used in a class annotated with `@Controller`, causes the response to be
rendered as JSON. Otherwise, returning a String will cause Spring to look for
an HTML template. This annotation is not needed when using `@RestController`.

`@RequestBody`  
When added to a method argument, this annotation indicates that the object
exists in the body of the request. For example, when POSTing a User object
encoded in JSON.

`@Valid`  
Indicates that a method argument should be validated. How the validation occurs
will depend on if you implemented the `Validator` interface or if you used
JSR-303 annotations.

`ResponseEntity`  
Wraps an object to return on the response. The type of object returned can be
expressed via type arguments. `ResponseEntity` also gives you control the status
code of the response.

```
// Specifies a User is returned.
private ResponseEntity<User> someMethod() { ... }

// Specifies a List of Users is returned.
//Note that the generic type parameters can be nested.
private ResponseEntity<List<User>> someMethod() { ... }

// Can be used without type parameters.
private ResponseEntity someMethod() { ... }             
```

## Testing

`@Test`  
Add this annotation to a method to turn it into a test.

`@SpringBootTest`  
Annotates a class with tests to add all of Spring's capabilities.

`@AutoConfigureMockMvc`  
Adds a `MockMvc` class to the ApplicationContext to help test web applications.

`@ActiveProfiles`  
Annotates a class, enabling the given profiles for all the tests within the
class. Useful for testing out different application configurations.
