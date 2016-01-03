# ICCS474
## Internet Programming

## Server Side and Client Side

![Image](https://raw.githubusercontent.com/SaKKo/muic-iccs474-2015t2/master/assets/server-client.png)

### Simplest way to host a file.

- First check if you have python in your computer
    - `python --version`
    - If it shows command not found then you have to install python first.
    - Python is bundled to every mac by default.
- To start a simple http server.
    - Create a folder in your workspace directory.
        - I recommended that you start workspacing your computer by
        - create a folder at `~/_workspace`
        - keep all your codes separated in to project names in `~/_workspace` eg. `~/_workspace/iccs474/simple_http_server`
    - `cd ~/_workspace/iccs474/simple_http_server`
    - `touch index.html`
        - Modify file's content using `vim`, `atom`, `nano`, or `subl`
        - You can just `echo` (which will append) text into file by using this command.
            - `echo "Hello World" >> index.html`
    - Start the server
        - `python -m SimpleHTTPServer 8888`
    - open your favorite browser and browse to `http://localhost:8888`
        - You can also try `http://your-friend-ip:8888`

> Now let's discuss what is actually happening.

### HTML

- ?

### CSS

- ?

### JS

- ?
