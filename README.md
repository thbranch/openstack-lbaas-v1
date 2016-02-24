# openstack-lbaas-v1

This is to add neutron lbaas to a existong openstack instalation either kilo or liberty - if on liberty check out v2
I will be adding some automation with ansible soon 

controller node:
1) packages
apt-get isntall:
python-neutron-lbaas
neutron-lbaas-common

2) servies
  neutron-openvswitch-agent.service
  neutron-ovs-cleanup.service
  neutron-server.service

3) config files

***********************************
neutron.conf
[DEFAULT]
service_plugins =lbaas

***********************************
neutron_lbaas.conf
[DEFAULT]

[quotas]

[service_auth]

[service_providers]
service_provider=LOADBALANCER:Haproxy:neutron_lbaas.services.loadbalancer.drivers.haproxy.plugin_driver.HaproxyOnHostPluginDriver:default

[certificates]

###################################
network node:
1) packages
apt-get isntall:
python-neutron-lbaas
neutron-lbaas-common
neutron-lbaas-agent

2) servies
neutron-lbaas-agent.service

3) config files

***********************************
neutron.conf
service_plugins =lbaas

***********************************

neutron_lbaas.conf 
[DEFAULT]

[quotas]

[service_auth]

[service_providers]
service_provider=LOADBALANCER:Haproxy:neutron_lbaas.services.loadbalancer.drivers.haproxy.plugin_driver.HaproxyOnHostPluginDriver:default

[certificates]

***********************************
lbaas_agent.ini
[DEFAULT]
debug = False
interface_driver =neutron.agent.linux.interface.OVSInterfaceDriver
device_driver = neutron.services.loadbalancer.drivers.haproxy.namespace_driver.HaproxyNSDriver

[haproxy]
user_group = haproxy
