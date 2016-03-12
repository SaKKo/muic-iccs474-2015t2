# ICCS474
## Internet Programming

### SSL

- Secure Socket Layer
- Well explained here.
    - https://www.digicert.com/ssl.htm

> Based on Rails Security Best Practice
> http://guides.rubyonrails.org/security.html#cross-site-request-forgery-csrf

### Session Hijacking

- Stealing a user's session id lets an attacker use the web application in the victim's name
    - The session id is a 32 byte long MD5 hash value
    - How to steal?
        - It's normally done by using man-in-the-middle attack.
        - Full access to user's hardware
    - How to protect?
        - SSL 
            - Not 100% safe
            - Still vulnerable to man-in-the-middle attack

### Session Fixation

- Faking user session and make them think that they are using their own account while they are not.

![Image](https://raw.githubusercontent.com/SaKKo/muic-iccs474-2015t2/master/assets/session_fixation.png)

> This attack focuses on fixing a user's session id known to the attacker, and forcing the user's browser into using this id. It is therefore not necessary for the attacker to steal the session id afterwards. Here is how this attack works:
> 
> - The attacker creates a valid session id: They load the login page of the web application where they want to fix the session, and take the session id in the cookie from the response (see number 1 and 2 in the image).
> - They maintain the session by accessing the web application periodically in order to keep an expiring session alive.
> - The attacker forces the user's browser into using this session id (see number 3 in the image). As you may not change a cookie of another domain (because of the same origin policy), the attacker has to run a JavaScript from the domain of the target web application. Injecting the JavaScript code into the application by XSS accomplishes this attack. Here is an example: <script>document.cookie="_session_id=16d5b78abb28e3d6206b60f22a03c8d9";</script>. Read more about XSS and injection later on.
> - The attacker lures the victim to the infected page with the JavaScript code. By viewing the page, the victim's browser will change the session id to the trap session id.
> - As the new trap session is unused, the web application will require the user to authenticate.
> - From now on, the victim and the attacker will co-use the web application with the same session: The session became valid and the victim didn't notice the attack.

- How to protect?
    - Always reset user's session before login and after logout.
        - `reset_session`
    - Session Expiry
        - Since client can edit their own cookies, we need to store and expire sessions from server side.

### CSRF

![Image](https://raw.githubusercontent.com/SaKKo/muic-iccs474-2015t2/master/assets/csrf.png)

- Cross Site Forgery
    - Basically making request to server without using javascript or minimize using javascript. 
    - Example
        - GET
            - `<img src="http://www.webapp.com/project/1/destroy">`
        - MOUSE OVER Javascript
            - `<img src="http://www.harmless.com/img" width="400" height="400" onmouseover="dosomething()" />`
        - POST, Automatically sent
```        
            <a href="http://www.harmless.com/" onclick="
              var f = document.createElement('form');
              f.style.display = 'none';
              this.parentNode.appendChild(f);
              f.method = 'POST';
              f.action = 'http://www.example.com/account/destroy';
              f.submit();
              return false;">To the harmless survey</a>
```


- How do we protect our server from CSRF?
    - use GET, POST, PATCH, PUT or DELETE appropriately. 
        - Avoid get request that change application state.
    - a security token in non-GET requests will protect your application from CSRF
        - Beware of XSS
        - Include Authenticity Token for form POST.
            - In rails easily done by using, `protect_from_forgery with: :exception`

```
            rescue_from ActionController::InvalidAuthenticityToken do |exception|
              sign_out_user # Example method that will destroy the user cookies
            end
```

### Redirection
        
- Attacker manipulate the redirect uri to be a phishing website
    - INTENDED
        -  `http://www.example.com/site/redirect?to=www.mywebsite.com`
    - MODIFIED
        -  `http://www.example.com/site/redirect?to=www.attacker.com`
- Avoid allowing user to supply redirect uri

### File Uploads

- Make sure file uploads don't overwrite important files, and process media files asynchronously.
    - EG. `../../../etc/passwd`
- Executable Code in File Uploads
    - Source code in uploaded files may be executed when placed in specific directories. Do not place file uploads in Rails' /public directory if it is Apache's home directory.















