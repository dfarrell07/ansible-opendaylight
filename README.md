# OpenDaylight Ansible Role

Ansible role for the [OpenDaylight SDN controller][1].

**This project is new and under construction. See our [issue tracker](https://github.com/dfarrell07/ansible-opendaylight/issues) for details.**

## Requirements

The OpenDaylight Ansible role handles the installation and configuration of all of its dependences.

## Role Variables

### Karaf Features

To set extra Karaf features to be installed at OpenDaylight start time, pass them in a list to the `extra_features` variable. The extra features you pass will typically be driven by the requirements of your ODL install. You'll almost certainly need to pass some.

OpenDaylight normally installs a default set of Karaf features at boot. They are recommended, so the ODL Ansible role defaults to installing them. This can be customized by overriding the `default_features` variable. You shouldn't normally need to do so.

### Karaf Feature Repos

To configure additional repos to search for Karaf features, override the `extra_feature_repos` variable.

OpenDaylight comes with a pre-configured st of Karaf feature repos. They are recommended, so the ODL Ansible role defaults to installing them. This can be customized by overriding the `default_features` variable. You shouldn't normally need to do so.

### REST API Port

To change the port on which OpenDaylight's northbound listens for REST API calls, use the `odl_rest_port` variable. This was added because OpenStack's Swift project uses a conflicting port.

## Dependencies

The OpenDaylight Ansible role doesn't depend on any other Ansible roles.

## Example Playbook

The simple example playbook below would install and configure OpenDaylight using this role.

```yaml
---
- hosts: example_host
  sudo: yes
  roles:
    - opendaylight
```

To override default settings, pass variables to the `opendaylight` role.

```yaml
---
- hosts: all
  sudo: yes
  roles:
    - { role: opendaylight, extra_features: ['odl-ovsdb-openstack'] }
```

Results in:

```
opendaylight-user@root>feature:list | grep odl-ovsdb-openstack
odl-ovsdb-openstack                   | 1.0.3-Helium-SR3    | x         | ovsdb-1.0.3-Helium-SR3                   | OpenDaylight :: OVSDB :: OpenStack Network Virtual
```


## License

The OpenDaylight Ansible role is Open Sourced under a BSD two-clause license. Contributions encouraged!

## Author Information

[Daniel Farrell][2] of the [OpenDaylight Integration Team][3] is the main developer of this role.

See [CONTRIBUTING.md][4] for details about how to contribute to the OpenDaylight Ansible role.


[1]: http://www.opendaylight.org/project/technical-overview
[2]: https://twitter.com/dfarrell07
[3]: https://wiki.opendaylight.org/view/CrossProject:Integration_Group
[4]: https://github.com/dfarrell07/ansible-opendaylight/blob/master/CONTRIBUTING.md
