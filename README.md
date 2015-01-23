# Multi-Platform Ansible Role and Playbook Test VMs

I maintain [over 50 roles](https://galaxy.ansible.com/list#/users/219) on Ansible Galaxy, and a few dozen more locally. Since I run both CentOS (a RedHat derivative) and Ubuntu/Debian-based servers, I like to have a reliable platform to test my roles and playbooks everywhere with minimal effort.

On GitHub, I generally use Travis CI to run a minimal set of tests against the Travis CI environment (currently Ubuntu 12.04). I wrote about this setup on the Server Check.in Blog: [Testing Ansible Roles with Travis CI on GitHub](https://servercheck.in/blog/testing-ansible-roles-travis-ci-github). It's impossible to bootstrap extra test VMs inside the Travis environment due to Travis' use of OpenVZ. Thus, to run Ansible playbooks against CentOS and other versions of Ubuntu, I have to rely on a local configuration.

For this, I use Vagrant and some VirtualBox boxes that I build to follow the latest releases of the OSes I support. Currently, you can find the boxes I use on [Atlas](https://atlas.hashicorp.com/geerlingguy) (they are hosted at [files.midwesternmac.com](http://files.midwesternmac.com/)), and this project runs a playbook against the following OSes:

  - Ubuntu 12.04.x
  - Ubuntu 14.04.x
  - CentOS 6.x
  - CentOS 7.x

The project is extremely simple, and simply requires [Vagrant](https://www.vagrantup.com/), [VirtualBox](https://www.virtualbox.org/), and [Ansible](http://docs.ansible.com/intro_installation.html) to be installed on your host machine.

## Testing a Role

To test a role, the role must be installed on your host machine (you can install galaxy roles via `$ ansible-galaxy install [rolename]`, but this project is more focused on testing roles you'd be working on locally). Just add the role to `playbook.yml` and run `vagrant up`.

It should take a few minutes to download each of the base boxes the first time, but after that, it takes about a minute to boot each VM, then run the playbook with your role(s).

After testing a role, you can destroy the four VMs with `vagrant destroy -f`. You can also just build one particular VM with `vagrant up ubuntu1204` (as an example), or re-run the ansible playbook with `vagrant provision ubuntu1204`.

## License

MIT

## Author Information

Created in 2014 by [Jeff Geerling](http://jeffgeerling.com/), author of [Ansible for DevOps](http://ansiblefordevops.com/).
