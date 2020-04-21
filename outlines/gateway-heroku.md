* Introduce Gateway
  * Demo code-based configuration
  * Demo the need for ForwardedHeaderFilter
* Heroku
  * Documentation
    * `./gradlew build -x test`
  * How to run the project using gradlew
  * How to build the project using gradlew
  * Heroku Java 11
  * Heroku Procfile
  * Using the correct port with ${PORT}
    * Emphasize the need for different profiles
  * Create new app
    * Link to GitHub
    * Use automatic deploys
    * Do a manual deploy
    * Take a look at the logs
  * Attaching a database
    * Addons -> Heroku Postgres
    * Requires custom work to create data source
    * Postgres considerations: @Lob
* Heroku command line tool
  ```
  heroku login
  heroku apps
  heroku pg --app cybr406-Post
  heroku pg:reset --app cybr406-account --confirm cybr406-account
  heroku logs --tail --app cybr406-post
  ```
