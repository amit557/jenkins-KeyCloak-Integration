# Jenkins-KeyCloak-Integration
This project provides a pre-configured environment to demonstrate Single Sign-On (SSO) for the Jenkins UI and Bearer Token Authentication for the Jenkins REST API using Keycloak.

Prerequisie: Windows System with atleast (8GB RAM), Latest Docker Desktop installed on it.

Below address will used: 
http://localhost:8081   Jenkins    Version 2.541.1
http://localhost:8080   KeyClock  Version 26.5.3


Use attached docker compose file.


On cmd type:  D:<Path>/docker compose up -d

KeyCloak Setting:
1. Create Realm --> "jenkins"
2. Realm → Clients → Create client {Client Type: OpenID Connect, Client ID: jenkins} Next
3. Capability config --> Client authentication On || Standard flow On
   Valid redirect URIs: http://localhost:8081/securityRealm/finishLogin
   Web origins: http://localhost:8081  (Save)
   Clients → jenkins → Credentials → Copy Secret
   
4. Users → Create user  Username: demo-user Enabled: ON Set password (not temporary).
   

Jenkins Settings:
Jenkins → Manage Jenkins → Plugins → Available
OpenID Connect Authentication Plugin & Bearer Token Authentication Plugin (for REST API
Jenkins → Manage Jenkins → Configure Global Security

Security Realm:
Login with OpenID Connect

Client ID	jenkins
Client Secret	(copied from Keycloak)
Configuration mode   Discovery via well-known endpoint
Well-known configuration endpoint "http://keycloak:8080/realms/jenkins/.well-known/openid-configuration"
Advanced Override scopes: openid

Note: If required update hosts file.

Test UI Login
---------------
Open Incognito hit Jenkins url http://localhost:8081

Click Login --> Redirects to Keycloak
Login as demo-user
Redirects back to Jenkins ✅

🎉 Jenkins UI login via Keycloak works
