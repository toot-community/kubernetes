# Fastly Logging Verification with Kubernetes Ingress

This repository contains a Kubernetes Ingress configuration used for Fastly logging verification for
the `fluent-bit.toot.community` domain.

Fastly requires domain control proof for logging to a HTTPS endpoint. It achieves this through an HTTP challenge on a
well-known path. The challenge path must return a 200 response including the hex representation of the SHA-256 of your
Fastly service ID.

## Kubernetes Ingress Object

The Ingress object in this repository, named `fluent-bit-fastly-verify`, is configured to handle HTTP requests at the
path `/.well-known/fastly/logging/challenge` for the host `fluent-bit.toot.community`. It is set to return a 200 status
code with the SHA-256 representation of Fastly service IDs as a response.

These IDs are included directly in the Ingress configuration under
the `nginx.ingress.kubernetes.io/configuration-snippet` annotation:

```
return 200 "4f2f2e79f3bc04cdcf388a833fa24fc7d7d9c116bab870966fd0a8ca282ad480\nd4b239774c478b6dd780918b276d6102edb71c4d2f02d91ad9abfca3eab6f3a4";
```

The Ingress uses the `letsencrypt-prod` cluster issuer for the SSL certificate and is configured to use the `fluent-bit`
service on port `2020` for the backend. The Ingress object is managed under the `fluentbit` namespace.

This configuration ensures Fastly can verify domain control for logging by making an HTTP GET request to
the `.well-known` path and receiving the appropriate SHA-256 service ID representation in the response.
