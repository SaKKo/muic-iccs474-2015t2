# ICCS474
## Internet Programming

### Deploy

- The simplest way to deploy would be with heroku.
    - Why should or shouldn't we use heroku?
- Deploying from scratch.
    - Many services to choose from.
        - AWS
        - GCP
        - DigitalOcean
        - Linode
    - Simplest OS to use Ubuntu Server 14.04 LTS
    - WebServer
        - The first entrance to your application from the internet.
        - Capable of serving static files or act as load balancer.
        - Example
            - nginx
            - apache
    - AppServer
        - It's just an application
            - load your (rails) application
            - serve your (rails) application on a port or socket
            - control the processes/threads of your application.
        - Example
            - passenger
            - puma
            - unicorn
            - thin
        - Each has pros and cons, it's always good to do some research before using any.
        - Process vs Thread
            - Thread are spawns inside process.
            - If a thread is blocked, you can start a new thread to serve new request using that same process.

- Installation
    - ssh-key
        - `ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`
        - Private vs Public key
    - Starting up a server
        - starts a digital ocean droplet.
        - ssh to your droplet, and starts by upgrading OS to latest version.

        ```
        ssh root@xxx.xxx.xxx.xxx
        sudo apt-get update
        sudo apt-get upgrade
        sudo reboot
        # ssh back to server
        ssh root@xxx.xxx.xxx.xxx
        ```

        - Adding new user, so we don't have to use root.

        ```
        adduser sakko
        gpasswd -a sakko sudo # Add sakko to sudo group
        exit # logout
        ```

        - Now that we have new user `sakko` let's ssh back in without using `root`
        - Notice that we need to input password. Let's also fix that to use authorized_keys

        ```
        ssh sakko@xxx.xxx.xxx.xxx
        # In your server
        mkdir ~/.ssh
        exit

        # back to local
        # copy public key to `.ssh/authorized_keys`
        cat ~/.ssh/id_rsa.pub | ssh sakko@xxx.xxx.xxx.xxx 'cat >> .ssh/authorized_keys'

        # try ssh back in, it shouldn't ask for you password
        ssh sakko@xxx.xxx.xxx.xxx
        # protect your key
        chmod 600 ~/.ssh/authorized_keys
        ```

        - Removing permission to login for root and changing default port

        ```
        # in your server
        sudo vim /etc/ssh/sshd_config
        # SET `Port 22` to `Port 1555`
        # SET `PermitRootLogin no`
        # exit vim
        sudo service ssh restart # warning, if you did something wrong above, you might not be able to login again.
        # logout
        exit

        # try ssh back in, with specific port
        ssh -p 1555 sakko@xxx.xxx.xxx.xxx
        ```

        - Firewall, it is always good to protect your server from the outside world.

        ```
        sudo ufw allow 1555/tcp   # for ssh
        sudo ufw allow 80/tcp
        sudo ufw allow 443/tcp    # only for ssl, if your app is running on https
        sudo ufw show added
        sudo ufw enable
        ```

        - Setup timezone for your server because your application is running based on that time.
        - You might want to install and learn more about NTP later.

        ```
        sudo dpkg-reconfigure tzdata
        ```

        - If you are on a small instace with limited RAM.
        - SSD are considered as cheap RAM, we can create swap file so that we have some extra memory.
        - Run this line by line and ensure that there is no error.

        ```
        sudo fallocate -l 4G /swapfile
        sudo chmod 600 /swapfile
        sudo mkswap /swapfile
        sudo swapon /swapfile
        sudo sh -c 'echo "/swapfile none swap sw 0 0" >> /etc/fstab'
        sudo reboot
        sudo swapon -s
        ```

    - `SaKKo` general Application Set
        - You don't have to use everything I setup here.

        ```
        sudo apt-get install git-core tmux vim htop libcurl4-openssl-dev 
        # optional (if you are using rails or nodejs)
        sudo apt-get install nodejs ntp postgresql libpq-dev autopostgresqlbackup
        # install Redis, Memcached, ImageMagick, etc based on your application needs
        ```

    - Installing nginx

        ```
        sudo apt-get install nginx

        # Getting your server ip via command line

        ip addr show eth0 | grep inet | awk '{ print $2; }' | sed 's/\/.*$//'
        ```

        - Open browser and browse to your public IP
        - Nginx is serving a default static page.
        - Nginx preload application in memory. If you reloaded code, you have to restart your webserver.

        ```
        sudo service nginx stop|start|restart
        ```

        - You can ensure that nginx is started everytime server rebooted by running.

        ```
        sudo update-rc.d nginx defaults
        # if it's already enabled then it will alert you with
        # System start/stop links for /etc/init.d/nginx already exist.
        # removing /etc/init.d/nginx will stop nginx from starting during startup
        ```

    - Deploying Static Pages
        - Create a static page folder

        ```
        # in your server
        cd ~
        mkdir static_pages
        cd static_pages
        vim index.html
        ```

        - `index.html` content

        ```
        <!DOCTYPE html>
        <html lang="en">
        <head>
          <meta charset="UTF-8">
          <title>Hello world</title>
        </head>
        <body>
          Hello world
        </body>
        </html>
        ```

        - Linking nginx config

        ```
        sudo vim /etc/nginx/nginx.conf

        # look for 
        include /etc/nginx/sites-enabled/*.conf;
        ```

        - Nginx is setup to load every config files located inside site-enabled
        - But we will not be creating config directly in that folder.
        - We will add configs into sites-available folder then symlink the file that we want to site-enabled.

        ```
        cd /etc/nginx/sites-available
        touch static_pages.conf
        # copy content of nginx/nginx.static.conf (located in my github) into static_pages.conf
        ```







