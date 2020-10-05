# tfgen-python

Generate Terraform Libvirt Provider - Using jinja2 template

Libvirt Provider: https://github.com/dmacvicar/terraform-provider-libvirt

# Development

I'm using j2cli to test out j2 template

# What this repo needs?

* Python code to generate multiple files by running single command
For example:

`tfgen --data example-data.yml --output-dir foo`

example-data.yml
```yml
spec:
  - name: vm1 
    hostname: vm1
    nested_enabled: true
    vcpus: 1
    memory: 1024M
    console: vnc
    cloud_data:
      user:
        - name: root
          public_key:
            - ssh-rsa example root@host1
            - ssh-rsa example root@host2
        - name: user1
          password: strongpassword
          public_key:
            - ssh-rsa example user1@host
            - ssh-rsa example user2@host
    cloud_image:
      storage_pool: isos
      name: template-ubuntu.img
    disk:
      storage_pool: default
      disk:
        - name: vm1-vda.qcow2
          size: 10G
          storage_pool: vms
        - name: vm1-vdb.qcow2
          size: 10G
          storage_pool: vms
    network:
      - name: net-10.10.10
        address: 10.10.10.10
        mtu: 1500
        gateway: 10.10.10.1
        dns: [8.8.8.8, 8.8.4.4]
  - name: vm2 
    hostname: vm2
    nested_enabled: false
    vcpus: 1
    memory: 1024M
    console: vnc
    cloud_data:
      user:
        - name: root
          public_key:
            - ssh-rsa example root@host1
            - ssh-rsa example root@host2
        - name: user1
          password: strongpassword
          public_key:
            - ssh-rsa example user1@host
            - ssh-rsa example user2@host
    cloud_image:
      storage_pool: isos
      name: template-ubuntu.img
    disk:
      storage_pool: default
      disk:
        - name: vm2-vda.qcow2
          size: 10G
          storage_pool: vms
        - name: vm2-vdb.qcow2
          size: 10M
          storage_pool: vms
    network:
      - name: net-10.10.10
        address: 10.10.10.10
        mtu: 1500
        gateway: 10.10.10.1
        dns: [8.8.8.8, 8.8.4.4]
```

Will create
```
foo
├── cloudinit1.cfg
├── cloudinit2.cfg
├── main.tf
├── network1_config.cfg
└── network2_config.cfg
```
