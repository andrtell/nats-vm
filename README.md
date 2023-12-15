# Nats VM

VM with a NATS server

## Basic VM

Setup you VM using [basic-vm](https://github.com/andrtell/basic-vm).

## Ansible

Create the file `inventory.yaml`.

```
ungrouped:
  hosts:
    vm:
      ansible_host: vm01
```

Create the file `vars.yaml`.

```
certs_fullchain: /etc/letsencrypt/live/example.com/fullchain.pem
certs_privkey: /etc/letsencrypt/live/example.com/privkey.pem
```

## NATS VM

Run all playbooks.

```
ansible-playbook -i inventory.yaml --ask-become-pass --extra-vars "@vars.yaml" --extra-vars="nats_token=secret" playbooks/*.yaml
```

## NATS

Check the connection

```
nats server check connection -s example.com --user=secret
```

Then try some pub/sub

```
nats sub msg -s nats://secret@example.com
```

```
nats pub msg "Hello, world" -s nats://secret@example.com
```
