# ansible-snmp

SNMP modules for [Ansible](http://www.ansible.com) to perform `get`, `getnext`, `getbulk`, `set`, `trap` and `inform` 
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
```

The `result` variable will contain SOMETHING ;-)

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
    auth_password: authkey1
    priv_protocol: aes256
    priv_password: privkey1
  register: result
```

## Usage

## Status

This module is currently in planning stage.

## Dependencies

This module requires [pysnmp](http://snmplabs.com/pysnmp/) to be installed.
