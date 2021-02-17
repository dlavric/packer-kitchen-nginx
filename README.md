# Repository for learning Kitchen.ci

## This Repository tests with Kitchen.ci if the Ubuntu box has the nginx installed

## Instructions

### Prerequisites
- [X] [VirtualBox](https://www.virtualbox.org/wiki/Downloads)

- [X] [Vagrant](https://www.vagrantup.com/downloads)

- [X] [Packer](https://www.packer.io/downloads)

- [X] Ruby

How to install Ruby on MacOS Catalina:

```shell
$ brew install rbenv

$ echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.zshrc
$ echo 'eval "$(rbenv init -)"' >> ~/.zshrc

$ source ~/.zshrc
```

Install the 2.6.6 version of Ruby and check the version:

```
$ rbenv install 2.6.6

$ rbenv local 2.6.6

$ rbenv versions

$ bundle install
```


## How to Use this Repo

- Clone this repository:
```shell
$ git clone git@github.com:dlavric/packer-nginx64.git
```

- Go to the directory where the repo is stored:
```shell
$ cd packer-nginx64
```

- Start Packer:
```shell
$ packer build template.json
```

- Add the box to Vagrant: 
```shell
$ vagrant box add --name xenial64 xenial64-vbox.box
```

- Initialize Vagrant with the local box created with Packer:
```shell
$ vagrant init -m xenial64
```

- Start Vagrant
```shell
$ vagrant up
```

- Open a new terminal and deploy the cookbook code for Kitchen:
```shell
$ bundle exec kitchen converge
```

- Check the virtual box is known to Kitchen:
```shell
$ bundle exec kitchen list
```

- Deploy the test to check if nginx is installed on the xenial64 box:
```shell
$ bundle exec kitchen verify
```

Output:
```zsh
Profile: tests from {:path=>"/Users/daniela/Downloads/dlavric/packer-kitchen-nginx/test/integration/default"} (tests from {:path=>".Users.daniela.Downloads.dlavric.packer-kitchen-nginx.test.integration.default"})
Version: (not specified)
Target:  ssh://vagrant@127.0.0.1:2202

  System Package nginx
     ✔  is expected to be installed

Test Summary: 1 successful, 0 failures, 0 skipped
       Finished verifying <default-vbox-xenial64> (0m1.93s).
-----> Test Kitchen is finished. (0m2.96s)
```

- Delete the Kitchen instance once finished:
```shell
$ bundle exec kitchen destroy
```

- Destroy the Vagrant machine:
```shell
$ vagrant destroy
```