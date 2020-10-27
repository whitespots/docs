# SDLC \(Secure Development Lifecycle\)

## Development pipeline

### 1. Feature idea

Let's imagine that we have an idea to implement a new registration flow.  
Business target:  
- Increase registration conversion

**Details**:  
- User needs to input only email  
- After submitting the form he should be redirected to his account  
...

> _\(From security\)  
> -_ User can not do anything important without email verification  
> **Risks:**  
> - User account takeover  
> - Reputation damage  
> - ..

**Security practices**

{% page-ref page="practices-implementation/design/design-review.md" %}

It can be helpful here, if your team has any questions:

{% page-ref page="practices-implementation/security-champions.md" %}



### 2. Specification

Now we need to understand, how will we solve this task technically and create all required tasks.

Details:  
- \[Backend\] Change required registration form inputs  
- \[Backend\] Implement password generation  
...

> _\(from security\)_   
> - \[Backend\] reCaptcha on registration  
> - \[Backend\] make generated passwords temporary  
> - ..

**Security practices**

{% page-ref page="practices-implementation/design/design-review.md" %}

It can be helpful here, if your team has any questions:

{% page-ref page="practices-implementation/security-champions.md" %}

### 3. Development & Testing

After development knows what to do, features will be developed and tested.   
We need to implement 2 **Security practices** here

{% page-ref page="practices-implementation/implementation/code-review.md" %}

{% page-ref page="practices-implementation/implementation/implementation-review.md" %}

It can be helpful here, if your team has any questions:

{% page-ref page="practices-implementation/security-champions.md" %}

After each step, the R&D team should have an understanding of the code and implementation quality.  
That's why it's very important to send them as better and as more detailed reports as you can.  
**The feature is not on production yet** and it can be easily fixed before any risks occur.

### 4. Production

Great!  
All risks were mitigated by the proper design review and all issues were resolved before the production deployment.  
But actually, it's not the last phase.

Finally, we really need to monitor all suspicious activity and look for anything we missed during the previous steps.

**Security practices**

{% page-ref page="practices-implementation/asset-discovery.md" %}

{% page-ref page="practices-implementation/bugbounty.md" %}

## Have questions?

Write to us and get a **free** consultation.

**Website**: [whitespots.io](https://whitespots.io/?utm=appsecwiki)   
**Email**: [sales@whitespots.io](mailto:sales@whitespots.io)

