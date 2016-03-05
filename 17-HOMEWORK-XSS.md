# ICCS474
## Internet Programming

### Cross-site scripting (XSS)

Cross-site scripting (XSS) is a type of computer security vulnerability typically found in web applications. XSS enables attackers to inject client-side script into web pages viewed by other users.

Concept is explained in class.

- Create a project to demonstrate how XSS works using rails.

- Guideline
    - Use Devise to login as multiple users.
    - Create a model called `Blog` with content:text user:references
    - When user a create a Comment, try creating content with `<script></script>` inside.
    - When another user try to browse to `blogs/:id`, try rendering content as HTML instead of plain text. hint: use `raw`, `<%==  %>`, `sanitize`, or `.html_safe`

- Homework
    - Push to git repo and invite `sakko`
    - Explain in readme.md
        - How to install the project.
        - Which render function is the safest?
