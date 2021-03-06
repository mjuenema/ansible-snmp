# ansible-snmp

Generic SNMP modules for [Ansible](http://www.ansible.com) to perform `get`, `getnext`, `getbulk`, `set`, `trap` and `inform` 
operations and emulate `walk`.

## Examples

The following examples query the [snmplabs](http://snmplabs.com/snmpsim/public-snmp-agent-simulator.html) 
public SNMP simulation service.

### SNMPv2c Get

```
- name: Retrieve sysName and sysLocation with SNMPv2c
  snmp_get:
    oid: 
      - 1.3.6.1.2.1.1.5.0
      - 1.3.6.1.2.1.1.6.0
    host: demo.snmplabs.com
    port: 161
    version: 2
    community: public
    timeout: 1
    retries: 5
  register: result
  
- debug:
    msg: "sysLocation {{ result.varbinds[1][1] }}"
```

* `result.error_indication` will be `True` on an SNMP engine error.
* `result.error_status` will be `True` on an SNMP PDU error.
* `result.error_index`, if non-zero refers to `result.varbinds[errorIndex-1]`.
* `result.varbinds` will contain a list of (oid, value) tuples.

### SNMPv3 Set

```
- name: Retrieve sysName with SNMPv3
  snmp_set:
    oid: .1.3.6.1.2.1.1.5.0
    value: myhostname
    host: demo.snmplabs.com
    port: 161
    version: 3
    engine_id:
    security_level: authpriv
    security_name: usr-sha384-aes256
    auth_protocol: sha384
    auth_key: authkey1
    priv_protocol: aes256
    priv_key: privkey1
  register: result
```

## Usage

## Status

This module is currently in planning stage.

## Dependencies

This module requires [pysnmp](http://snmplabs.com/pysnmp/) to be installed.

## References

This module has been inspired by the [ansible-snmp](https://github.com/networklore/ansible-snmp) module by 
the [Networklore](https://networklore.com/) people.

There are several device specific SNMP modules for Ansible and you should use those over this module whenever possible.
* [ansible-cisco-snmp](https://github.com/networklore/ansible-cisco-snmp)
