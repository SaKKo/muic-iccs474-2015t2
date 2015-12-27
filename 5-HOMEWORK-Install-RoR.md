# ICCS474
## Internet Programming

### Install Ruby on Rails (RoR)

If your OS is outdated, it is a good time to update.

Clean installation is recommended. It is very very difficult to ensure that all the installed libraries are working properly if you don't clean install.
- Backup your files.
- Create an installation USB of El Capitan.

Follow these instructions to install RoR
https://github.com/SaKKo/install-ruby-on-rails-osx/blob/master/4.2.x.md

- DO NOT install `rvm` twice!
    - Try running `rvm --version`. If it failed, then you don't have `rvm` installed yet.
    - avoid using `sudo` command. You won't need to use `sudo` at all to install RoR. (if you search online, there are people who tell you to do <strike>`sudo gem install rails`</strike>. Do not do this, it is bad.)
- `rvm` is a tool to manage ruby environment.
    - check current ruby version by
        - `ruby --version`
    - You can try installing many ruby version
        - `rvm install 2.1`
        - `rvm install 2.2`
    - then swap between these 2 versions by running
        - `rvm use 2.1`
        - `rvm use 2.2`
        - `rvm use 2.2 --default`
