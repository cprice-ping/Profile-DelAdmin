This Server profile shows a complete install of PF \ PD with the Delegated Administator service and application configured.

The Delegator is installed and delivered via PingDirectory.  

`https://{{PD_DELEGATOR_PUBLIC_HOSTNAME}}:1443/delegator`

PingFed is configured with 2 OAuth clients:
* PingLogon -- used to authenticate a user and issue tokens (AuthZ Code \ Implicit)
* PingIntrospect -- used to validate tokens (PD has a PF Access Token Validator pointing to this client)

A set of PD users are also created and assigned Delegated Administrator roles:

These users are created in `ou=Administrators` to demonstrate separating the Admins from the objects they have rights to.

**Super Administrator**  
`SuperAdmin` \ `2FederateM0re`

**User Administrator**  
`UserAdmin` \ `2FederateM0re`

**Group Administrator**  
`GroupAdmin` \ `2FederateM0re`  
This user is a member of the `DelAdmins` group that is used to delegate the Group resources

This stack can be used as the basis of Delegated Admin Use Cases.

Delegated Objects are managed using the PingData console:  

`https://{{PingDataConsole}}:8443/console`

* Server: `pingdirectory`
* User: `Administrator`
* Pwd: `2FederateM0re`

PingFederate needs a couple of additional options:

* Virtual Host -- `pingfederate`  (Used for the backchannel ATV call from PD)
* OAuth AS --> Allowed Origins -- `https://${PD_DELEGATOR_PUBLIC_HOSTNAME}`  (Used to allow Delegator to call OIDC endpoints)
* PingLogon client is configured for Implicit and a wildcard `redirect_uri`

## Deployment - Docker Compose
Environment variables in the `env_vars-sample` can be modified to inject the correct locations into this stack. Rename this to `env_vars` for it to be read by `docker-compose.yaml`

To implement this Use Case, download the `docker-compose.yaml` file and run `docker-compose up -d`

DelAdmin trace logging has been enabled:  
https://support.pingidentity.com/s/document-item?bundleId=pingdirectory-73&topicId=hld1564011489908.html

The logs can be seen with this command:  
`docker-compose exec pingdirectory tail -f /opt/out/instance/logs/debug`
