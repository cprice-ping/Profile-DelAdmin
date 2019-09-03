This Server profile shows a complete install of PF \ PD with the Deletegated Administator service and application configured.

The Delegator is installed and delivered via PingDirectory.

PingFed is configured with 2 OAuth clients:
* PingLogon -- used to authenticate a user and issue tokens (AuthZ Code \ Implicit)
* PingIntrospect -- used to validate tokens (PD has a PF Access Token Validator pointing to this client)

[A PD user is also created and assigned Delegated Administrator roles]

[DelAdmin \ 2FederateM0re]