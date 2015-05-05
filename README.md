# Custom Policy Cookie and External Service Example

[JWT custom policy example using cookies]

# Mule version
Examples:
Mule 3.6.1

# Use Case
This is an example of a custom policy where the JWT token validation would be an external http service.
1. Client initiates the call.
2. When it hits Anypoint Gateway the policy will invoke.
3. The custom policy will retrieve the JWT token from the cookie and send that to an external validation service.
4. In this example the validaiton service is mocked by this flow validate.jwt.token exposing the endpoint http://0.0.0.0:8881/auth/jwt/verify.
5. The service will add an additional cookie called "addedCookie"
6. The custom policy validates that the JWT token is valid and stores the new "addedCookie" as a variable.
7. A call is being made to the mocked backend service. The backend service is mocked by the flow mock.backend.service exposing the endpoint http://0.0.0.0:8883/backend.
8. Before the response is being sent back to the client the cookie from the auth service is added to the response. 

# Installation 
Upload custom policy and yml file as custom policy. These can be found src/main/resources/policy/jwt.
Create a new API where you proxy backend service.
Download application to the gateway runtime.
IMPORTANT: Add this element: <http:connector name="HTTP-shared-connector" enableCookies="true"/>
By default cookies are not supported by the HTTP connector provided in gateway.

Sample provided in:
src/main/resources/proxy/app/config/proxy.xml

# Run
If the details in the proxy application is used then the main service can be invoked by running this command:
curl -v --cookie "jwt=eyJhb" http://0.0.0.0:8080/test
