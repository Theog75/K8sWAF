# Kubernetes WAF - Apache api gateway

This configurations shows how to create a dockerized (but can easily be created as a non-containerized deployment) imlementation of an Apache based API gateway.

The use case for which this configuration was made was to perform as an abstraction layer before the Kubernetes cluster in which to allow for the Following features to be added to applications running on the Kubernetes cluster.

## Features

- Authentication abstraction easily allowing ANY authentication method supported by apache (https://httpd.apache.org/docs/2.4/howto/auth.html and additional such as mod_kerb, SAML, OpenID ...)
- filtering by ip address / subnet
- WAF by using mod_sec OWASP 2.0 rules (https://owasp.org/www-project-modsecurity-core-rule-set/)

Apache has many more features which my be added to the feature list such as SSL support, and rewriting URLs etc. in order to implement them in this gateway configuration it is merely required to add configuration.

## High availability

there are several options to make this deployment highly available, either by deploying a number or deployment and putting a load balancer in front of them or using keepalived (https://www.keepalived.org) are my favorites.

## Quick setup

Pull this repository to your home directory (or anywhere else).

To deploy this configuration just run:

```
docker run -it -p 80:8080 -v ~/apache-gateway/auth:/etc/httpd/conf.d theog75/k8swaf
```

on your local machine and point your browser to [http://localhost/v2](http://localhost)

## Configuration

### Virtualhosts

The file rct.co.il.conf in the auth directory can be configured to add / modify additional virtualhosts (the default is all hosts) and forward them to whichever targets you wish.

### authentication

Authentication in this example is done using basic auth (htpasswd) but can be modified or combine multiple authentication methodologies to different paths / virtual hosts.

To add users simple perform the following command:

```
htpasswd auth/htpasswd <username>
```

And type the password you wish for the user.

### groups

The file host.groups contains the groups and the users related to them - again this is using basic configuration but can easily be done to accommodate groups from LDAP or Active Directory or anywhere else.