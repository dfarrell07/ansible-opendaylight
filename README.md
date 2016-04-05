[![CI Status][7]][6]

# OpenDaylight Ansible Role

Ansible role for the [OpenDaylight SDN controller][1].

Releases of this role can also be installed available via [Ansible Galaxy][5].

## Requirements

The OpenDaylight Ansible role handles the installation and configuration of
all of its dependences.

## Role Variables

### Karaf Features

To set extra Karaf features to be installed at OpenDaylight start time,
pass them in a list to the `extra_features` variable. The extra features
you pass will typically be driven by the requirements of your ODL install.
You'll almost certainly need to pass some.

OpenDaylight normally installs a default set of Karaf features at boot.
They are recommended, so the ODL Ansible role defaults to installing them.
This can be customized by overriding the `default_features` variable. You
shouldn't normally need to do so.

### REST API Port

To change the port on which OpenDaylight's northbound listens for REST API
calls, use the `odl_rest_port` variable. This was added because OpenStack's
Swift project uses a conflicting port.

The Ansible role will handle opening this port in FirewallD if it's active.

## Dependencies

The OpenDaylight Ansible role doesn't depend on any other Ansible roles.

## Example Playbook

The simple example playbook below would install and configure OpenDaylight
using this role.

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
    - role: opendaylight
      extra_features: ['odl-ovsdb-openstack']
```

Results in:

```
opendaylight-user@root>feature:list | grep odl-ovsdb-openstack
odl-ovsdb-openstack | 1.1.0-Lithium | x | ovsdb-1.1.0-Lithium <snip>
```

## License

The OpenDaylight Ansible role is Open Sourced under a BSD two-clause license.

[Contributions encouraged][4]!

## Author Information

[Daniel Farrell][2] of the [OpenDaylight Integration Team][3] is the main
developer of this role.

See [CONTRIBUTING.md][4] for details about how to contribute to the
OpenDaylight Ansible role.


[1]: http://www.opendaylight.org/project/technical-overview
[2]: https://twitter.com/dfarrell07
[3]: https://wiki.opendaylight.org/view/CrossProject:Integration_Group
[4]: https://github.com/dfarrell07/ansible-opendaylight/blob/master/CONTRIBUTING.md
[5]: https://galaxy.ansible.com/list#/roles/3948
[6]: https://travis-ci.org/dfarrell07/ansible-opendaylight
[7]: https://travis-ci.org/dfarrell07/ansible-opendaylight.svg
