* Introduction to desired functionality
* Account must share users
  * New "check-user" endpoint
  * Supply a username and password to get authorities
  * Limit to only a few roles
* Post must use Account to verify user and get authorities
  * Create a new `AuthenticationManager` implementation
* RestConfiguration
  * WebClientBean
* AccountAuthenticationProvider
