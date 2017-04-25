# Ansible HashMerge potential issue

The documentation (http://docs.ansible.com/ansible/intro_configuration.html#hash-behaviour) shows that when ```hash_behaviour = merge``` is set - then two hashes with the same name should be merged.

However this simple code apparently shows they don't in practice.

## To run

```ansible-playbook -i inventories test.yml```

## Result

```
TASK [debug] *******************************************************************
ok: [localhost -> localhost] => {
    "changed": false,
    "msg": [
        {
            "description": "Frontend for all HTTPS traffic",
            "name": "https"
        }
    ]
}
```

## Expected result

```
TASK [debug] *******************************************************************
ok: [localhost -> localhost] => {
    "changed": false,
    "msg": [
        {
            "description": "Frontend for all HTTPS traffic",
            "name": "https"
        },
        {
            "description": "Frontend for all HTTP traffic",
            "name": "http"
        }
    ]
}
```

## Test version

# ansible --version
```
ansible 2.3.0.0
  config file = ansible.cfg
  configured module search path = Default w/o overrides
  python version = 2.7.12 (default, Nov 19 2016, 06:48:10) [GCC 5.4.0 20160609]
```
