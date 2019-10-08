This Server profile shows a complete install of PF \ PD with the Delegated Administator service and application configured.

The Delegator is installed and delivered via PingDirectory.  

`https://{{PingDirectory}}:1443/delegator`

PingFed is configured with 2 OAuth clients:
* PingLogon -- used to authenticate a user and issue tokens (AuthZ Code \ Implicit)
* PingIntrospect -- used to validate tokens (PD has a PF Access Token Validator pointing to this client)

A PD user is also created and assigned Delegated Administrator roles

`DelAdmin` \ `2FederateM0re`

This is a Super Admin that can see and manage **all** Users and Groups 

This stack can be used as the basis of Delegated Admin Use Cases.

Delegated Objects are managed using the PingData console:  

`https://{{PingDataConsole}}:8443/console`

* Server: `pingdirectory`
* User: `Administrator`
* Pwd: `2FederateM0re`

PingFederate needs a couple of additional options:

* Virtual Host -- `pingfederate`  (Used for the backchannel ATV call from PD)
* OAuth AS --> Allowed Origins -- `https://${DELEGATOR_PUBLIC_URL}`  (Used to allow Delegator to call OIDC endpoints)
* PingLogon client is configured for Implicit and a wildcard `redirect_uri`

## Deployment - Docker Compose
Environment variables in the `docker-compose.yaml` can be modified to inject the correct locations into this stack

To implement this Use Case, download the `docker-compose.yaml` file and run `docker-compose up -d`
