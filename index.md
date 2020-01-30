# Communication

* Ry Lowry (lowryrs@unk.edu)
* [Slack](https://cybr406-2020.slack.com)
* [Syllabus](/files/cybr406-syllabus-2020.pdf)

# Resources

* [Spring Boot Initializer][] - Generate project skeletons.
* [Common Spring Properties][] - Adjust the many settings provided by Spring.
* [Spring Reference][] - Annotations, classes, and files used in class.
* [IDE Survival Guide][] - Useful IDE tips & tricks.

# Software

* [IntelliJ Community Edition][] - The IDE we will use in class.
* [7Zip][] - Unzip archives easily.
* [Putty][] - If you want to try manually crafting requests.
* [Postman][] - A nice REST GUI.
* [Atom][] - A good text editor.
* [Git][] - Version control.

# Class Log

| Date | Topic | Notes |
|------|-------|-------|
| 01-14-2020 | Class Introduction | Introduced class and started discussing requests. |
| 01-16-2020 | Environment Setup | **[Homework 1](/homework/cybr406-hwk1.docx) Due 01-21-2020 End of Day**.<br/>Used classtime to set up software & accounts.<br/>Used class time to experiment with requests using echo server.
| 01-21-2020 | Spring Basics | Questions about Homework<br/>Finish setting up environments<br/>**Presentation: [Spring Basics][]** |
| 01-23-2020 | Spring Basics (cont.) | Continue Spring Basics<br/>**Demo App: [Spring Basics][]** |
| 01-28-2020 | Spring Basics (cont.) | Finish Spring Basics. |
| 01-30-2020 | Todo Project | **[Todo Project](https://github.com/ryl/cybr406-todo) Due 02-04-2020 End of Day**<br/>**Work Day:** Put your knowledge of the basics to work in a project. |
| 02-04-2020 | Todo Project (cont.) | Another day of in class work.<br/>Discuss how to submit project for grading. |

# Class Topics

**January**

* Class Introduction
* HTTP Requests
* Environment Setup
* Working with Gradle Projects
* Spring Basics
* Unit Testing
* Testing with mocks
* In-memory Databases
* Persisted Databases
* Database Migrations

**February/March**

* Gateways
* Basic Security
  * In memory user details
  * Roles
  * Securing URLs
  * Http basic
* Pitfalls
  * CSRF, HTTP Basic, and Sessions
  * SQL Injection
  * XSS
* Advanced Security
  * Access security information within a controller.
  * Access security information from arbitrary class.
  * Method level security for extra granularity
  * Managing users in the database.
* Custom Security
  * Pre-authorized tokens.

**March/April**

* Working with a UI
* CORS
* OAuth2

<!-- Resources -->
[Spring Boot Initializer]: https://start.spring.io
[Common Spring Properties]: https://docs.spring.io/spring-boot/docs/current/reference/html/common-application-properties.html
[WizTools RESTClient]: https://github.com/wiztools/rest-client/releases/download/3.7.1/restclient-ui-fat-3.7.1.jar
[Postman]: https://www.getpostman.com
[Heroku Project Setup]: /notes/heroku-project-setup.md
[GitHub + Heroku Project Setup]: /notes/github-project-setup.md
[Git]: https://git-scm.com/downloads
[IntelliJ Community Edition]: https://www.jetbrains.com/idea/
[7Zip]: https://www.7-zip.org/
[Putty]: https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html
[Atom]: https://atom.io/

<!-- Files -->
[Spring Basics]: /files/spring-boot-basics.pptx

<!-- Notes -->
[Database Migrations]: /notes/database-migrations.md
[Spring Data REST]: /notes/spring-data-rest.md
[Gateways]: /notes/gateways.md
[Security - Basics]: /notes/security-basics.md
[Security - Advanced]: /notes/security-advanced.md
[Security - Checklist]: /notes/security-checklist.md
[open-house]: /notes/open-house.md
[Event Handler Shortcomings]: /notes/event-handler-shortcomings.md
[Security - OAuth]: /notes/security-oauth.md
[blog-wrap-up]: /notes/blog-odd-and-ends.md
[Spring Reference]: /notes/spring-reference.md
[IDE Survival Guide]: /notes/ide-survival-guide.md

<!-- Demos -->
[Books Demo]: https://github.com/ryl/cybr406-books
[Spring Basics]: https://github.com/ryl/cybr406-basics

<!-- Homework -->
[Homework 2]: /homework/homework02-persisted-database.md
[Homework 3]: /homework/homework03-user-security.md
[Homework 4]: /homework/homework04-user-oauth.md
[project]: /homework/project.md
