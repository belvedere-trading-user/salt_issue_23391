# salt_issue_23391

This is a simple Vagrant setup that recreates the following Salt issue:
https://github.com/saltstack/salt/issues/23391

Install Vagrant (www.vagrantup.com for help)

To recreate the issue:

1. Download the vagrant box: 'vagrant box add https://atlas.hashicorp.com/puppetlabs/boxes/centos-6.6-64-puppet'
2. Startup the vagrant environment: `vagrant up`
3. Login to the Vagrant server: `vagrant ssh`
4. Run pillar.item and pillar.get for the "python" pillar (they'll return identical results):
 1. `sudo salt saltmaster1 pillar.item python`
 2. `sudo salt saltmaster1 pillar.get python`
5. Update the python pillar: `sudo cp /srv/pillarroot/python/basedata.b /srv/pillarroot/python/basedata.sls`
6. Run pillar.item and pillar.get for the "python" pillar (they'll return different results):
 1. `sudo salt saltmaster1 pillar.item python`
 2. `sudo salt saltmaster1 pillar.get python`
7. Run a refresh_pillar: `sudo salt saltmaster1 saltutil.refresh_pillar`
8. Run pillar.item and pillar.get for the "python" pillar (they'll return different results):
 1. `sudo salt saltmaster1 pillar.item python`
 2. `sudo salt saltmaster1 pillar.get python`
