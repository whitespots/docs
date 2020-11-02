# OAuth 2.0

## General info

OAuth allows a **resource provider**, to request access to a user’s resources from an **identity provider** with user’s approval.   
It's an **authorization** framework

## Terms

**Resource Provider \(RP\)**  
\(Usually the website in scope for the engagement\)

**Identity Provider \(IDP\)**  
\(Usually an external service like Google, GitHub, or Facebook\)

**Client\_id**  
The client\_id is unique to each **RP** and allows the **RP** to identify itself to the **IDP**.

{% hint style="info" %}
The Client\_Id is **public** and identifies this RP to the IDP.
{% endhint %}

**Access Token**  
An access token is a multiple use string issued by the **IDP** which can be directly used to access the user’s resources stored on the **IDP**

**Client Secret**  
The Client Secret is unique to each **RP** and allows the **RP** to exchange valid code and state combinations for **Access Tokens** at the **IDP**.

{% hint style="info" %}
The Client Secret must always be **kept secret**! If it ever leaks, attackers can subvert the OAuth flow by converting codes into tokens. This allows them to access the resources at the IDP directly instead of accessing them through the RP.
{% endhint %}

**Authorization Code**  
This code is a single use string which can be combined with a valid **State** and **Client Secret** and exchanged at the **IDP** for an **Access Token**. You cannot use this code to access a user’s resources at the **IDP**, it must first be exchanged for an **Access Token**.

{% hint style="info" %}
It’s important to point out here that Code != Access Token. An authorization code cannot be used to directly make requests to the IDP and must be exchanged for an access token by the RP.

The Authorization Code will be passed from the Browser to the RP, who will exchange it with the IDP for an Access Token.

This Code cannot be used to receive an Access Token from the IDP unless it is paired with the RP’s Client Secret.
{% endhint %}

**State**  
The State is private and should be unique per OAuth session. It is essentially a CSRF Token and should be protected accordingly.

{% hint style="info" %}
The RP must validate that the State received from the Browser is the same as the State sent in step 2 for CSRF protection.
{% endhint %}

**Redirect URI**  
The Redirect URI is the location where the **IDP** will send the Browser after completing the auth dance. When the Browser is directed here, it will contain the **Authorization Code** and the **State**.

{% hint style="info" %}
The Redirect URI should be registered with the IDP and constrained to a single value or to a pattern match.
{% endhint %}

## Flows

### Authorization Code 

![](../../../../../.gitbook/assets/image%20%285%29.png)

### 

1. The Browser selects a provider, let’s say GitHub, in the application and clicks “Connect to GitHub”.
2. The **RP** receives this request and redirects the Browser to the **IDP** along with a public **Client\_Id, a Redirect URI and a State**.
3. The Browser accepts the redirect and goes to the **IDP** endpoint.
4. The **IDP** responds and asks for the user to authenticate and to approve the scope of the OAuth request \(scope here meaning, repo level, admin level…\)
5. The Browser sends authentication information and approves the scope of the OAuth request.
6. The **IDP** directs the Browser to the **Redirect\_URI** along with the **Code** and the **State**.
7. The Browser follows the redirect to the **RP’s** OAuth endpoint and passes along the **Code** and the **State**.
8. The **RP** makes a call to the **IDP** attempting to exchange a **Code**, **Client\_Id**, **Redirect\_URI**, and **Client Secret** for an **Access Token**.
   * Don’t confuse this Redirect\_URI with the one used in Step 2. This will probably not be modifiable as the RP does not send this request through the browser.
9. If the **Client Secret** and **Code** are valid for the given **Client\_Id**, then the **IDP** will return an **Access Token** to the **RP**.
10. Now the **RP** wants to access the user’s resources. They can simply call the **IDP** endpoint with the **Access Token as a parameter**. This is usually done via a custom header.
11. If the **Access Token** is valid, the **IDP** will return that user’s resources.

### Authorization Code with Proof Key for Code Exchange \(PKCE\)

![Picture from OAuth0.com](../../../../../.gitbook/assets/image%20%286%29.png)

{% hint style="info" %}
**App = RP  
Auth0 Tenant = IDP**
{% endhint %}

1. The user clicks **Login** within the application.
2. **RP** creates a cryptographically-random `code_verifier` and from this generates a `code_challenge`.
3. **RP** redirects the user to the **IDP** \(**/authorize** endpoint\) along with the `code_challenge`.
4. **IDP** redirects the user to the login and authorization prompt.
5. The user authenticates using one of the configured login options and may see a consent page listing the permissions will give to the application.
6. **IDP** stores the `code_challenge` and redirects the user back to the application with an authorization `code`, which is good for one use.
7. **RP** sends this `code` and the `code_verifier` \(created in step 2\) to the **IDP** \(**/oauth/token** endpoint\).
8. **IDP** verifies the `code_challenge` and `code_verifier`.
9. **IDP** responds with an ID Token and Access Token \(and optionally, a Refresh Token\).
10. **RP** can use the Access Token to call an API to access information about the user.
11. The API responds with requested data.

[**Other flows**](https://auth0.com/docs/flows)\*\*\*\*

## Recommendations

1. Use whitelists for your urls
2. Make temporary things really temporary
3. Pay attention to configuration
   1. Cookie flags - **secure**, **httponly**, **samesite**
   2. `Cache-Control: no-store` header for each response with tokens
4. Never pass your tokens in `Referrer` header
5. Use limits for all brutable tokens

## Attacks & Testing

### Referer Header Leaks Code + State

Ensure that after the IDP’s redirect to the RP, the Referer header is stripped of URL parameters or even removed if possible. This will prevent the attack scenario detailed below

1. If at any point after the redirect to the RP, you see the code and state in the Referer header, then the site is vulnerable.

### Insufficient URI Validation

1. Follow the flow until the Step 2 with `redirect_uri` parameter
2. Edit it like in following examples:
   1. aws.console.amazon.com/**myservice** → aws.console.amazon.com
   2. **aws**.console.amazon.com/myservice → console.amazon.com/myservice
   3. **aws.console.amazon.com**/myservice → evil.com/myservice
3. If the Browser is redirected, then the site is vulnerable to this attack.

{% hint style="info" %}
Make sure to verify that the site doesn’t trim the Referer header or otherwise strip the URL parameters. Otherwise the Code / State will be difficult to recover and this is just an open redirect
{% endhint %}

### Access Token Stored in Browser History / Cache

1. Open your browser’s history and cache and see if any of the Location entries contain sensitive information.

### State problems

Attackers can compose CSRF attacks with modified Redirect URIs and an attacker’s Code to authenticate the victim using attacker resources.

{% hint style="info" %}
If the victim does not realize that the authentication code has been swapped, they may place sensitive data inside attacker controlled resources. The reason this attack works is because the state parameter in step 2 is unique to a session. If there is no state provided at step 2 of the OAuth flow there is nothing to verify the session token against.
{% endhint %}

#### Lack of state

1. On the initial request to the IDP, verify that the state value is passed as a URL parameter.
2. Continue stepping through the OAuth Flow until the Redirect URI is reached.
3. Ensure that the Redirect URI has the state as a URL parameter.
   * Ensure that if the service has multiple OAuth Endpoints or bounces after the Redirect URI, that the final hop actually passes the state to the backend RP.

#### Reused

1. On the initial request to the IDP, view the State value passed as a URL parameter.
2. Repeat this process, verifying that the State variable has been changed between requests.

{% hint style="info" %}
It’s important to test this in the case that OAuth succeeds and in the case where OAuth fails, either because the user rejected the scope, or because the Redirect URI didn’t go to the expected RP OAuth Endpoint.
{% endhint %}

#### Invalid validation

1. On the initial request to the IDP, modify the State parameter passed as a URL parameter by changing it to an invalid value.
2. Complete the OAuth Flow, and validate that the returned code and invalid state are rejected by the RP.
3. Repeat steps 1-3 but omit the state variable altogether. Ensure that the RP rejects the response from the IDP.

#### Insecure

The State variable should be treated like a CSRF token. If the value used for State is predictable or otherwise brute forcible, than it’s possible that an attacker could make multiple CSRF attacks in an automated fashion and brute force authenticate a user with attacker resources.

1. On the initial request to the IDP, view the State value passed as a URL parameter.
2. Repeat this process, verifying that the State variable has sufficient entropy and is not otherwise predictable

### Reusable authorization codes

Check to see if an RP will let a user redeem the same authorization code multiple times. Each code should only be good for a single OAuth session, reusing a code which has already been redeemed should result in an error.

1. Complete an entire OAuth process. Track the authorization code provided by the IDP, save this value.
2. Select the same OAuth provider, Start Intercepting, Press Connect Button.
3. Complete the OAuth Flow, and validate that the returned code is different from the code received in step 1.
4. Replace the returned code with the code saved in step 1.
5. Ensure that the OAuth process fails, either via rejection from the RP or the IDP.

## References

Many thanks to:

* [Authorization code flow pentest guide](https://maxfieldchen.com/posts/2020-05-17-penetration-testers-guide-oauth-2.html)
* [RFC 6749](https://tools.ietf.org/html/rfc6749)
* [OAuth0](https://OAuth0.com)



