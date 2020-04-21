# Heroku and Gradle

* Heroku builds the app using the command `./gradlew build -x test`
* Must specify JDK 11 in `system.properties` file
* Must create a Procfile
  * Contains the command executed to start you app
* Must use the port Heroku provides
  * Available in the environment variable PORT
