# osm-slackbot-ansible

Ansible Project for [OSM Slack Bot](https://github.com/osmlab/osm-slackbot).

## Description

This is an [Ansible](https://www.ansible.com/) project for the easy deployment of [OSM Slack Bot](https://github.com/osmlab/osm-slackbot).  OSM Slack Bot (a Slack bot for [OpenStreetMap](http://openstreetmap.org/)) queries the [Humanitarian OpenStreetMap Team Tasking Manager](https://github.com/hotosm/osm-tasking-manager2) and the [OSM API](https://api.openStreetMap.org/api/0.6/).  Learn more in the [OSM Slack Bot Readme](https://github.com/osmlab/osm-slackbot/blob/master/README.rst).

## Installation

On your control machine, you'll first need to install [Ansible](https://www.ansible.com/).

### Ansible

To install ansible follow the commands below.  For more information, see the [Getting Ansible](http://docs.ansible.com/ansible/intro_installation.html#getting-ansible) section of the Ansible docs.

The easiest way to install ansible for Ubuntu or Mac OS X is:

```
sudo easy_install pip
sudo pip install ansible
```

If upgrading ansible, then do:

```
sudo pip install ansible --upgrade
```

### Vagrant / Virtual Box

If using [Vagrant](https://www.vagrantup.com/) and/or [Virtualbox](https://www.virtualbox.org/), see their relevant documentation

### OSM Slack Bot

After installing ansible and configuring your enviornment, simply clone this repo onto your control machine to get started, such as below.

```
git clone https://github.com/osmlab/osm-slackbot-ansible.git osm-slackbot-ansible.git
```

## Usage

First, create a `secret.yml` [YAML](https://en.wikipedia.org/wiki/YAML) file in the root project directory and add the auth token you got from Slack, which is currently found on Slack at "Browse apps > Custom Integrations > Bots"

```
---

SLACK_AUTHTOKEN: "XXXX"
```

This token will be automatically added to a local_settings.py file on provision.  The auth token is uniquely assigned to your Slack team, so no other team identifier is needed.

**Stop words**

You can edit your stop words, in your all.yml file.

### Vagrant

To launch a vagrant machine, simply do:

```
# cd into project directory
vagrant up
```

If re-provisioning, then do:

```
vagrant provision
```

### EC2

First, create a `hosts` file in the project root directory.  The hosts file can be as simple as the public IP address of your ec2 machine.

```
##.##.##.##
```

Learn more about managing your inventory at http://docs.ansible.com/ansible/intro_inventory.html.  This hosts file will be referenced in the command below.

Run the following command to provision your ec2 instance.  Be sure to replace `~/osm-slackbot-1.pem` below with the path to your actual key for the machine.

```
# cd into project directory
ansible-playbook --user=ubuntu --connection=ssh --timeout=30 --inventory-file=hosts -v --private-key=~/osm-slackbot-1.pem --extra-vars=@extra_vars/ec2.yml --extra-vars=@secret.yml ec2.yml
 ```
