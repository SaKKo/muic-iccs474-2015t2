# ICCS474
## Internet Programming

### Install Ruby on Rails (RoR)

- Worth 2% of your grade.
    - 2% if you got it to work properly. regardless of OS version.
    - 1.5% if you clean installed your pc and didn't get it to work.
    - 1% if you didn't clean install and didn't get it to work.
    - 0% for any other cases.
- Due 18 January 2015 (Beginning of class)

### If your Mac OS is OUTDATED, it is a good time to update and a good time to learn how to do it. (skip this if you are on ubuntu)

Clean installation is recommended. It is very very difficult to ensure that all the installed libraries are working properly.

As a developer, you must be able to at least do a clean install for your mac. It has one of the most simplest installation process.

If you don't want to update/reinstall your OS, then stay with your current OS version until the end of term. Or use Virtual Machine for this class.

- Backup your files.
- Create an installation USB of El Capitan.
- Boot from USB and use disk utility to erase all partitions.
- Create a new partition.
- Install OS to that partition.

### Follow these instructions to install RoR

- MAC
    - https://github.com/SaKKo/install-ruby-on-rails-osx/blob/master/4.2.x.md
    - Don't forget to download/install `nodejs`

- Ubuntu
    - Same as MAC but install nodejs by running `sudo apt-get install nodejs` (yes use `sudo`)

>-

# IMPORTANT NOTE

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

### Ensure that RoR is working

- run `cd ~/Desktop`
- run `rvm use 2.2 --default`
- run `rails new hello_world` (make sure there is internet)
- run `cd ~/Desktop/hello_world`
- run `bundle install` (run it until everything passed)
- run `rails s`
- open chrome and navigate to `localhost:3000` and you should see a rails app running.
