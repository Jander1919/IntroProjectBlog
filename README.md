## BLOG Server & Web
This is the web application server and web app client for BLOG. The purpose of this application is to connect our database to an API. It also serves our web client application and our web admin panel.

## Configuring your local environment
In order to contribute to development of the BLOG web app, you'll need to set-up your local environment. If you run into issues in this process be sure to check the troubleshooting section of this README. It's likely that your issue has a solution that is covered in this section.

### Step 1 - Vagrant and Virtualbox
Grab the latest version of vagrant + virtualbox and install them on your local machine before continuing.
* [Vagrant Download](http://downloads.vagrantup.com/)
* [Virtualbox Download](https://www.virtualbox.org/wiki/Downloads)

### Step 2 - Initializing your local git repo
You should clone the git repo for this project on your local machine somewhere before continuing.

### Step 3 - Launching the virtual machine
Now that you have the codebase, vagrant and virtualbox on your machine, it's time to launch your virtual machine. The following command will launch your VM as well as run a provisioning script which will install all project dependencies.

    vagrant up

### Step 4 - Connecting to your virtual machine
Once your VM is up and running you will need to connect to it. To do this we do the following:

    vagrant ssh

### Step 5 - Setting up your environment variables
Ask someone for all the exact exports you need for this step. You will need to place these export command in the file below. After you edit this file, ensure that your reload your profile so the environment variables exist.

    vim /home/vagrant/.profile
    source /home/vagrant/.profile

### Step 6 - Configuring your ruby environment
Once you `ssh` into your VM after setting up your environment variables, we need to install all ruby libraries. To do this run the bundle command below:

    sudo gem install bundler -v 1.9.6
    bundle install

### Step 7 - Setting up your database
Once your ruby environment is initialized you will need to configure your local postgresql database. To do this copy and paste the following set of commands into your console. Ensure you `ssh` before running this.

    sudo su postgres
    pg_dropcluster --stop 9.1 main ; pg_createcluster --start --locale en_US.UTF-8 9.1 main
    exit
    sudo -u postgres createuser -s blog_development
    sudo -u postgres psql -c "ALTER USER blog_development WITH PASSWORD 'blog_development'"

### Step 8 - Provisioning your database
Now that your database configuration has been set you should provision your database with our applications schema and test data. Run the following set of commands to do this.

    rake db:create
    rake db:migrate
    rake db:seed

### Step 9 - Launching the web server
At this point all resources have been installed and initialized and you are ready to start your rails server. To do this use the following command:

    rails s -b 30.30.30.11

## Working with Rails tests
As of Rails 4.1 you must maintain your test database/environment manually. Run the following commands to ensure that happens. The migration step must be run each time the database schema updates.

    RAILS_ENV=test;bundle exec rake db:create;RAILS_ENV=development
    RAILS_ENV=test;bundle exec rake db:migrate;RAILS_ENV=development
    RAILS_ENV=test;bundle exec rake test:prepare;RAILS_ENV=development

Once migrated, you can run the tests with the following command:

    RAILS_ENV=test;bundle exec rake test;RAILS_ENV=development

Finally, if you would like to run a specific test we use the `m` gem for this as follows:

    RAILS_ENV=test;bundle exec m test/functional/controllers/api/v4/companies_controller_test.rb:13;RAILS_ENV=development

## Using the virtual machine
Variant and virtualbox are not difficult to use. Below are some general commands to help you in managing your local VM.

This first set of commands should be your basic operating commands.

    vagrant up - Boot the VM (or awake from sleep mode)
    vagrant ssh - Connect to the VM
    exit - Exit the VM
    vagrant suspend - Put the VM into sleep mode

If you run into issues with your VM, you can always hard shutdown your VM with the following command:

    vagrant halt -f

Finally, if your VM is locking up often or in general running very slow then it might be time to destroy and rebuild your VM.

    vagrant destroy -f

## Using GIT with BLOG
We have some general rules that we like to follow when using GIT with BLOG. So long as we follow the below rules then we should never have to do any cherry picking or difficult merging.

### Rule 1 - Don't cross-merge branches
If `branch-a` and `branch-b` are both branched off of `master`, `branch-a` and `branch-b` should never be merged into any branch but master. Adhering to this strict hierarchy rule will avoid any question of what code is where, and we should avoid cross-merging all together.

### Rule 2 - Stick to the following commands
Git is not a complicated system and you should never have to do things like rebasing so long as you stick to the following command set.

    git init
    git fetch
    git remote
    git checkout
    git add -A
    git commit
    git status
    git pull
    git push
    git merge

## Troubleshooting the Web Server
VMs and their providers (virtualbox) can sometimes misbehave. If you run into issues with the above process, don't panic, you're not the first to run into issues. Below are some issues along with some general solutions to problems you may run into.

### VM Boot issues
If you run into issues when booting your VM, don't panic. The issue very well may be that you need to restart the virtualbox instance. The following command will reboot that instance, keep in mind the file path, yours may be installed somewhere else.

    sudo /Library/StartupItems/VirtualBox/VirtualBox restart

### PostgreSQL Issues
Sometimes your local postgre server can run into issues. Most often this just requires a restart of that server.

    sudo /etc/init.d/postgresql restart

### ElasticSearch Issues
Sometimes your local ElasticSearch server can run into issues. Most often this just requires a restart of that server.

    sudo /etc/init.d/elasticsearch restart

### NPM Issues
Having issues with `npm`? Duh, it's `npm`. Below are a bunch of commands that have fixed various issues we have come across with `npm` in the past.

If you are having file/folder permission issues, I find it useful to chown the locations you will be writing to:

    sudo chown -R $USER /usr/local
    sudo chown -R $USER /vagrant/node_modules
    sudo chown -R $USER:$GROUP ~/.npm

If that doesn't work then you may need a more spagetti-like approach. Run the following commands:

    sudo npm cache clean -f
    sudo npm install -g n
    sudo n stable