This Server profile shows a complete install of PF \ PD with the Delegated Administator service and application configured.

The Delegator is installed and delivered via PingDirectory.
https://{{pingdirectory}}:1443/delegator

PingFed is configured with 2 OAuth clients:
* PingLogon -- used to authenticate a user and issue tokens (AuthZ Code \ Implicit)
* PingIntrospect -- used to validate tokens (PD has a PF Access Token Validator pointing to this client)

A PD user is also created and assigned Delegated Administrator roles

DelAdmin \ 2FederateM0re

This is a Super Admin that can see and manage **all** Users and Groups.

This stack can be used as the basis of Delegated Admin Use Cases.

Delegated Objects are managed using the PingData console:
https://localhost:8443/console

Server: pingdirectory
User: Administrator
Pwd: 2FederateM0re

Things of note:
PingFederate needs a couple of additional options:

Virtual Host -- `pingfederate`  (Used for the backchannel ATV call from PD)
OAuth AS --> Allowed Origins -- `https://localhost:1443`  (Used to allow Delegator to call OIDC endpoints)