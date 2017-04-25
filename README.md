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
