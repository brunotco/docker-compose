# Traefik

## Create authentication credentials
To use basic http authentication, you will need a credential that's `username:password` where the `password` is hashed.

To create the credential run :

```
# Replace username and password with what you want
echo $(htpasswd -nb username password) | sed -e s/\$/\$\$/g
```

This will create a string that you can copy to use as the credentials, the `$` need to be escaped by adding another `$` that's what the pipe in the command for.
