# Spring Reference

A list of concepts, annotations, classes, and files used in class.

## Bootstrapping

* [Using the @SpringBootApplication Annotation](https://docs.spring.io/spring-boot/docs/current/reference/html/using-spring-boot.html#using-boot-using-springbootapplication-annotation)

#### @SpringBootApplication
Annotates the class containing your program's main method. Initializes various
default settings.

#### SpringApplication  
Class with helper methods to launch your application. Used in your application's
main method.

## Dependency Injection

Features for configuration, class dependencies, and code reuse.

* [Java-based Container Configuration](https://docs.spring.io/spring/docs/current/spring-framework-reference/core.html#beans-java)
* [Annotation-based Container Configuration](https://docs.spring.io/spring/docs/current/spring-framework-reference/core.html#beans-annotation-config)

#### ApplicationContext
A big "tool bag" containing many "tools". The tools are classes configured by
Spring or your application. It is the central interface to provide configuration
for an application. Often referred to as the "Spring container".

#### @Configuration
Indicates that a class declares one or more `@Bean` methods.

#### @Bean
Indicates that a method produces a bean to be managed by the Spring container.
Similar to `@Component` in that the object returned by the method is added to
the `ApplicationContext` and can be `@Autowired` elsewhere. They appear within
classes annotated with `@Configuration`

#### @Component
Annotates a class for reuse throughout the application. Adds your class to the
tool bag (the `ApplicationContext`).

#### @Autowired  
Annotates a field indicating that class should be fetched from the
ApplicationContext. It marks the location where you want to use a tool from the
tool bag.

#### Profiles  
[Documentation](https://docs.spring.io/spring-boot/docs/current/reference/html/spring-boot-features.html#boot-features-profiles)  
Spring Profiles provide a way to segregate parts of your application
configuration and make it be available only in certain environments.

#### application.properties
[Documentation](https://docs.spring.io/spring-boot/docs/current/reference/html/spring-boot-features.html#boot-features-external-config-application-property-files),
[Profile-specific Properties](https://docs.spring.io/spring-boot/docs/current/reference/html/spring-boot-features.html#boot-features-external-config-profile-specific-properties)  
A file containing name/value pairs that configure the application. You can add
your own name/value pairs here to further customize your application. You can
configure different values for different profiles by creating additional
properties files following the naming convention
`application-{profile}.properties`.

#### @Value
[Documentation](https://docs.spring.io/spring-boot/docs/current/reference/html/spring-boot-features.html#boot-features-external-config),
[@Value Class Example](https://github.com/ryl/cybr406-gateway/blob/5f774348741fbe6929985d549a648ce2acea4add/src/main/java/com/cybr406/gateway/GatewayApplication.java#L13) with
[application.properties](https://github.com/ryl/cybr406-gateway/blob/master/src/main/resources/application.properties#L3)  
Inject a value from `application.properties` into a property in one of your
classes.

## Web

Features for handling web requests and returning responses.

* [Web Documentation](https://docs.spring.io/spring/docs/current/spring-framework-reference/web.html)
* [Validator Interface](https://docs.spring.io/spring/docs/current/spring-framework-reference/core.html#validator)
* [Validation Using JSR-303 Annotations](https://docs.spring.io/spring/docs/current/spring-framework-reference/core.html#validation-beanvalidation-overview)

#### @Controller, @RestController  
Annotate classes that handle web requests.

#### @RequestMapping
Annotates a method, describing which HTTP requests it should handle. By default
this annotation will map **ALL** HTTP methods to the Java method it annotates.
Be careful if this is not the behavior you expect. Most of the time, we only
intend for a Java method to respond to one and only one type of HTTP method.

#### @GetMapping, @PostMapping, @DeleteMapping, etc.
Like `@RequestMapping`, but only map requests for a specific HTTP method.
**Prefer one of these annotations** over `@RequestMapping` for their
specificity.

#### @RequestParameter  
Maps a request parameter to a method argument. By default, the name of the
method argument is expected to match the name of the request parameter.

#### @PathVariable  
Used in conjunction with `@RequestMapping` and its derivatives. Maps a portion
of the path to method argument.

#### @ResponseBody
When used in a class annotated with `@Controller`, causes the response to be
rendered as JSON. Otherwise, returning a String will cause Spring to look for
an HTML template. This annotation is not needed when using `@RestController`.

#### @RequestBody
When added to a method argument, this annotation indicates that the object
exists in the body of the request. For example, when POSTing a User object
encoded in JSON.

#### @Valid
Indicates that a method argument should be validated. How the validation occurs
will depend on if you implemented the `Validator` interface or if you used
JSR-303 annotations.

#### ResponseEntity
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

## Security

#### WebSecurityConfigurerAdapter  
* [Class Example](https://github.com/ryl/cybr406-books-demo/blob/master/src/main/java/com/cybr406/bookdemo/SecurityConfiguration.java#L22),
* [Configure HttpSecurity Example](https://github.com/ryl/cybr406-books-demo/blob/master/src/main/java/com/cybr406/bookdemo/SecurityConfiguration.java#L63-L78)

Main configuration class for customizing a web application's security settings.
Extend this class and override the `configure(HttpSecurity http)` method. Many
important security features can be adjusted from `configure` such as:

* Security requirements for URLS based on path, method, etc.
* enable/disable CSRF protection
* configure session management, or choose stateless

#### @EnableGlobalMethodSecurity

* [Documentation](https://docs.spring.io/spring-security/site/docs/current/reference/html5/#globalmethodsecurityconfiguration)
* [Class Example](https://github.com/ryl/cybr406-books-demo/blob/master/src/main/java/com/cybr406/bookdemo/SecurityConfiguration.java#L20)

Enables Spring Security global method security.

The `WebSecurityConfigurerAdapter::configure` method offers **broad** security
configuration options, but it has limitations. For example, you cannot easily
prevent one user from editing resources owned by another user.
`@EnableGlobalMethodSecurity` addresses the problem by giving you **granular**
control over when a Java method can be executed. Once global method security is
enabled, you can use `@PreAuthorize` and `@PostAuthorize` to finely adjust the
security requirements for a particular method.

#### @PreAuthorize

* [Documentation][Pre Post Authorize]

Adds a security expression to a method that must pass before the method will be
executed. May examine method arguments, but cannot access the method's return
value.

#### @PostAuthorize

* [Documentation][Pre Post Authorize]

Adds a security expression to a method that must pass after the method is
executed. Unlike `@PreAuthorize` this can examine the return value of the
method.

NOTE: We do not use this annotation in class. Most cases are covered by
`@PreAuthorize`.

#### HTTP Basic Authentication

* [Authorization Header Documentation](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Authorization)

HTTP Basic Authentication is a simple means of securing your application with a
username and password. Basic authentication uses the `Authorization` header with
a value of "Basic base64({username}:{password})".

It is important to realize the base64 is a means of encoding and **is not
encryption**. While a base64 does obscure the password's value, it is no more
secure than clear text. HTTP Basic Authentication **is only secure when coupled
with HTTPS**.

#### SQL Injection

* [Concept][SQL Injection Concept]
* [Class Example][SQL Injection Class Example]
* [XKCD Comic][]

A vulnerability that allows a malicious user to run SQL on the server. A
carefully crafted statement can cause sensitive data to be leaked, deleted, or
entire databases to be dropped. Often exploits SQL queries built using
String concatenation.

* [See the `updateNameDangerous` method for an example of a vulnerable method][SQL Injection Class Example].
* [More examples (scroll towards the bottom)][SQL Injection Concept]

This vulnerability can be fixed with **prepared statements**, which clearly
segment inputs from the rest of the SQL statement using a special placeholder
such as the '?' character.

* [See the `updateNameSafe` method for an example of a safe method][SQL Injection Class Example].

#### Cross Site Request Forgery (CSRF)

* [Concept][csrf concept]
* [Documentation][csrf documentation]
* [Synchronizer Token Pattern][]
* [When to use CSRF protection][]
* [Good Site][]
* [Bad Site][]

An attack that takes advantage of someone's existing logged in session on
another website. Bad Site demonstrates this by using hidden form fields to
submit a request to Good Site. If Good Site does not have measures in place to
prevent this abuse, Bad Site can transfer funds out of a victim's bank account.

This attack can be prevented by including a secret token in a request that only
[requiring a secret value][Synchronizer Token Pattern] that external websites
cannot guess. Spring has this form of CSRF protection **enabled by default.**

[In some cases, CSRF protection may not be necessary][When to use CSRF protection].
For example, stateless applications not meant to be accessed directly through a
browser (like the API's we create in class). In the case of the applications
written during this class, CSRF protection can be disabled when we make the
application stateless, which prevents our application from ever creating a
session with the client.

## Testing

#### @Test
Add this annotation to a method to turn it into a test.

#### @SpringBootTest
Annotates a class with tests to add all of Spring's capabilities.

#### @AutoConfigureMockMvc
Adds a `MockMvc` class to the ApplicationContext to help test web applications.

#### @ActiveProfiles
Annotates a class, enabling the given profiles for all the tests within the
class. Useful for testing out different application configurations.

[Pre Post Authorize]: https://docs.spring.io/spring-security/site/docs/current/reference/html5/#el-pre-post-annotations

<!-- CSRF References -->
[CSRF Concept]: https://owasp.org/www-community/attacks/csrf
[CSRF Documentation]: https://docs.spring.io/spring-security/site/docs/current/reference/html5/#csrf
[Synchronizer Token Pattern]: https://docs.spring.io/spring-security/site/docs/current/reference/html5/#csrf-protection-stp
[When to use CSRF protection]: https://docs.spring.io/spring-security/site/docs/current/reference/html5/#csrf-when
[Good Site]: https://github.com/ryl/cybr406-goodsite
[Bad Site]: https://github.com/ryl/cybr406-badsite

<!-- SQL Injection References -->
[SQL Injection Concept]: https://owasp.org/www-community/attacks/SQL_Injection
[SQL Injection Class Example]: https://github.com/ryl/cybr406-books-demo/blob/0849404fda2ebe4df503dd9adc12f5bbe469fdb5/src/main/java/com/cybr406/bookdemo/BookDemoController.java#L81-L92
[XKCD Comic]: https://xkcd.com/327/)
