ssh_pub
=========

Manage ssh pub keys.

Role Variables
--------------

`ssh_pub` expects a data structure similar to the following:

```
pub_keys: {
  "key_one": "ssh-rsa .....",
  "key_two": "ssh-ed25519 ...."
  "key_three": "ssh-ed25519 ...."
}
user_keys: {
  user: {
    keys: [
      "key_one",
      "key_two",
      "key_three"
    ],
    exclusive: true,
    hosts: {
      'host_two': {
        excludes: [
          "key_one"
        ]
      },
      'host_three': {
        excludes: [
          "key_one"
        ]
      }
    }
  },
  root: {
    keys: [
      "key_one"
    ],
    exclusive: false,
    hosts: {
      '*': {
        excludes: []
      }
    }
  },
}
```

The hosts specified in `user_keys[user]['hosts']` must be `inventory_hostname`,
it also only lets you specify excludes. Any host not in the dict will get the
pubkeys specified in the `keys` array.

Example Playbook
----------------

    - hosts: servers
      roles:
         - { role: qbit.ssh_pub }

License
-------

BSD
