# Red Team Summit Infra

This repo contains files supporting the RTS infrastructure.

Right now it's just one piece: the call for papers app
[Pretalx](https://github.com/pretalx/pretalx). We set this up using the Ansible
role [ansible-pretalx](https://github.com/pretalx/ansible-pretalx).

Installing it requires Ansible and a few supporting roles from Ansible Galaxy,
then the pretalx.yml playbook can be invoked which sets everything up.

## Pre-reqs & Setup

1. Clone this repo where the CFP site will live.
2. Edit pretalx.yml and set the TODO lines. For database password and Django
   secret key you can use any random string (get one from your password
   manager, `dd if=/dev/urandom bs=24 count=1 | base64`, or `uuidgen`).
3. [Install
   Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-the-control-node)
   this probably looks like `apt install ansible` or `dnf install ansible`.
4. Install the supporting roles:
```
$ ansible-galaxy install anxs.postgresql geerlingguy.certbot geerlingguy.redis
```
5. Install the ansible-pretalx role by cloning it in a subdirectory of where
   pretalx.yml lives:
```
$ git clone https://github.com/pretalx/ansible-pretalx
```
6. Point cfp.redteamsummit.com to this host.

## Running

To run the playbook and install all the things:
```
$ ansible-playbook pretalx.yml
```

To manually restart Pretalx:
```
# systemctl restart pretalx@event
```

* The config is written to `/home/pretalx_event/.pretalx.cfg`
* The logs are at `/usr/share/webapps/pretalxevent/data/logs/pretalx.log`
