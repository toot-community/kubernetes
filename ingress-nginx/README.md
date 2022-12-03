# Cloudflare Authenticated Origin Pulls

We're making Cloudflare authenticate itself to our origin servers, so we can ensure all traffic that hits our server is
coming from Cloudflare. This is a security measure to prevent malicious traffic from hitting our servers.

## Setting up the Origin Pull CA

```shell
$ wget https://developers.cloudflare.com/ssl/static/authenticated_origin_pull_ca.pem
$ kubectl create secret -n ingress-nginx generic cloudflare-authenticated-origin-pull-ca --from-file=authenticated_origin_pull_ca.pem
```

Configuration for actually checking the certificate is done in the `ingress-nginx` Helm chart.
