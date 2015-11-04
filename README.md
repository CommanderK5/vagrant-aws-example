Vagrant aws example
===================

Example Vagrantfile with [vagrant-aws plugin](https://github.com/mitchellh/vagrant-aws)

Require:
--------
vagrant
vagrant-aws plugin

Tested on Vagrant 1.7.4, vagrant-aws (0.6.0)

Usage:
-----

Rename configuration.yaml.template

`cp configuration.yaml.template configuration.yaml`

AWS access/secret keys 
```yaml
aws.access.key_id: 'AABBCCDDEEFFGG'
aws.secret_access_key: 'aabbccddeerrffddssaaxxccvvbbgghhjj'
```

Add nodes:

```yaml
nodes:
  node01:
    hostname: 'node01.aws.local'
    tags:
      Name: 'node01.aws.local'
      Role: 'master'
    secGroup: 'default'
    instance_type: 't1.micro'
  node02:
    hostname: 'node02.aws.local'
    tags:
      Business Unit: 'Corporate'
      Name: 'node02.aws.local'
      Role: 'slave'
    secGroup: 'default'
    instance_type: 't1.micro'
```

Run:
`vagrant up --provider=aws`
or
`vagrant up --provider=aws node01.aws.local`
