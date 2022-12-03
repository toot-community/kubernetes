# HAProxy

HAProxy is a TCP/HTTP load balancer. It is particularly suited for very high traffic web sites and powers quite a number
of the world's most visited ones.

## Mastodon

This setup uses HAProxy to connect to DigitalOcean's Redis instance, since Mastodon can't connect to TLS Redis
instances. **Be sure to change the ConfigMap to suite your needs.**

If Mastodon would support TLS Redis, this setup would be much simpler. HAProxy will probably be removed in the future.
