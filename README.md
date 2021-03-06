# Go Basic Auth

A fairly secure implementation of basic auth following some best practices improving security. Prompts you for a
password when accessing the protected route. Uses a custom middleware to implement basic auth guard.

Clone and set `AUTH_USERNAME` and `AUTH_PASSWORD` as environment variables.
```
  $ AUTH_USERNAME={YOUR_USERNAME} AUTH_PASSWORD={YOUR_PASSWORD} go run main.go
```

As this was a simple implementation, it wasn't connected to any Database. Also the reason SHA256 was used to hash the credentials. If storing them, a stronger hash should be chosen.

### Steps taken to improve security

1. Hash passwords and usernames to make their lengths obscure from an attacker.
2. Use `crypto.subtleTimeCompare` to check the entirety of the hashes before informing us of a match or mismatch.
3. Serve over HTTPS

### Routes

- [Unprotected route - `/`]("https://go-basic-auth.herokuapp.com/")
- [Protected route - `/dashboard`]("https://go-basic-auth.herokuapp.com/dashboard")

### Challenges

- Heroku's base tier does not allow me to serve with `.ListenAndServeTLS` because of challenges around obtaining a
  certificate and being able to reference that in the serve function. An explanation is found in
  this [Stack Overflow answer](https://stackoverflow.com/a/30501671/8294338).
