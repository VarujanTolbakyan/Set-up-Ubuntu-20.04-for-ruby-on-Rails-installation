# Set up Ubuntu 20.04 for ruby on Rails installation


## Step 1 - Installing rbenv and Dependencies


`$ sudo apt update`

### We are going to install all Ruby dependencies first.
`$ sudo apt install autoconf bison build-essential libssl-dev libyaml-dev libreadline6-dev zlib1g-dev libncurses5-dev libffi-dev libgdbm6 libgdbm-dev`

### Next, we are going to clone the official Rbenv repository into the home directory and add its binary to `$PATH` in order to use `rbenv` command line utility.



`$ git clone https://github.com/rbenv/rbenv.git ~/.rbenv`
`$ echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc`



### To load Rbenv automatically when the CLI starts.
`$ echo 'eval "$(rbenv init -)"' >> ~/.bashrc` or `echo 'eval "$(rbenv init -)"' >> ~/.zshrc`


### Then apply the changes you made to the ~ / .bashrc file for the current shell session
`$ source ~/.bashrc`


### Verify that `rbenv` is configured correctly with the type command, which displays additional information about the rbenv command

`$ type rbenv`

### The terminal window will display the following

`rbenv is a function
rbenv () 
{ 
    local command;
    command="${1:-}";
    if [ "$#" -gt 0 ]; then
        shift;
    fi;
    case "$command" in 
        rehash | shell)
            eval "$(rbenv "sh-$command" "$@")"
        ;;
        *)
            command rbenv "$command" "$@"
        ;;
    esac
}
`


### Then install the ruby-build plugin. This plugin adds rbenv install command to simplify the process of installing new Ruby versions.


`$ git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build`

******************************************************************************************************************************************

## Step 2 - Installing Ruby with ruby-build


First, let's list all available Ruby versions.

`$ rbenv install -l`

### Use `$ rbenv install --list-all / -L` to show all local versions.



### This command should display a long list of versions that you can install.

`$ rbenv install 2.7.3`

### Once the installation is complete, set the new version as the default Ruby version using the global subcommand.

`$ rbenv global 2.7.3`

********************************************************************************************************************************************


## Step 3 - Working with Gems

### Gems are a way to distribute Ruby libraries. You can use the `gem` command to manage this distribution. We use this command to install Rails.

### When installing the gem, the installation routine generates local documentation. This can significantly increase the installation time of the gem, so disable ### the generation of local documentation by creating ~ / .gemrc file with a configuration parameter to disable this feature:


`$ echo "gem: --no-document" > ~/.gemrc`


### Next, install the Bundler component as Rails depends on it.


`$ gem install bundler`


### You can use the gem env command (the `env` subcommand stands for environment) to learn more about the environment and gems configuration. You can see the gems ### installation location with the `home` argument, something like


`$ gem env home`


*******************************************************************************************************************************************


## Step 5 - Updating rbenv

### Since you installed `rbenv` manually using Git, you can update your installed version to the latest at any time by running the git pull command in the `~ /.rbenv` directory


`$ cd ~/.rbenv`
`$ git pull`


*****************************************************************************************************************************************


## Step 6 - Removing Ruby Versions

### After downloading additional Ruby versions, there may be too many versions in the ~ /.rbenv / versions directory. Use the uninstall subcommand in the ruby-## ### build plugin to remove unnecessary previous versions.

### For example, the following command will remove Ruby 2.1.3


`$ rbenv uninstall 2.1.3`


******************************************************************************************************************************************


## Step 7 - Removing rbenv

### If you decide not to use the rbenv utility anymore, you can uninstall it from your system.

### To do this, first open the `~/.bashrc` file in the editor.

`$ nano ~/.bashrc` or `vim ~/.bashrc`

### Find the following two lines in the file and delete them

...
`export PATH="$HOME/.rbenv/bin:$PATH"`
`eval "$(rbenv init -)"`


### Then uninstall `rbenv` and all installed Ruby versions with the following command

`rm -rf 'rbenv root'`


## ******* Installing Ruby on Rail and Dependencies **********


### Install the `curl` and other required packages for Ruby on Rails installation.

`$ sudo apt update`

`$ sudo apt install -y curl gnupg2 dirmngr git-core zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev software-properties-common libffi-dev`


### Install Node.js

### Rails need a Javascript runtime for application development in Linux. So, for that, we will install the LTS version of Node.js (v14.x).

`$ curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash -`

`$ sudo apt install -y nodejs`


### Install Yarn

### Add the Yarn repository in case if you want to install the Yarn package manager to manage packages.


`$ curl -sL https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -`

`$ echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list`



### Install Yarn with the below command.


`$ sudo apt update && sudo apt install -y  yarn`


### To install Rails, you need to use the gem install command with the -v flag to specify the version. For this tutorial we are using version 6.1.3:


`$ gem install rails -v 6.1.3`


##$ Note. If you want to install a different version of Rails, you can list the valid Rails versions by searching, which will return a long list of possible versions. Then we can install a specific version, for example 6.1.3:

`$ gem search '^rails$' --all`


`rbenv` creates a `shims` directory pointing to the files used by the currently active version of Ruby. Using the rehash subcommand, `rbenv` stores `shims` in this directory to match all Ruby commands across all installed Ruby versions on your server. When installing a new version of Ruby or a gem element that provides commands like Rails, use the following command



`$ rbenv rehash`

`$ rails -v`


