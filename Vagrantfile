# -*- mode: ruby -*-
# vi: set ft=ruby :
#
require 'yaml'

# Check required plugins
required_plugins = [ 'vagrant-aws' ]

required_plugins.each do |plugin|
  unless Vagrant.has_plugin?(plugin)
    system("vagrant plugin install #{plugin}")
  end
end

# Load global config
$configuration = YAML.load_file('configuration.yaml')

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  
  $configuration['nodes'].each do |key, val|

    config.vm.define val['hostname'] do |node|
      node.vm.box      = $configuration['config.vm.box']
      node.vm.box_url  = $configuration['config.box_url']
      node.vm.hostname = val['hostname']
      node.vm.provider "aws" do |aws|
        aws.security_groups = val['securitygroup']
        aws.tags            = val['tags']
        aws.instance_type   = val['instance_type']
      end
    end
  end
  
  config.vm.provider :aws do |aws, override|
    aws.access_key_id        = $configuration['aws.access.key_id']
    aws.secret_access_key    = $configuration['aws.secret_access_key']
    aws.keypair_name         = $configuration['aws.keypair_name']
    aws.region               = $configuration['aws.region']
    aws.ami                  = $configuration['aws.ami']
    aws.block_device_mapping = [{
      'DeviceName'              => $configuration['aws.block_device_mapping']['DeviceName'],
      'Ebs.VolumeSize'          => $configuration['aws.block_device_mapping']['Ebs.VolumeSize'],
      'Ebs.DeleteOnTermination' => $configuration['aws.block_device_mapping']['Ebs.DeleteOnTermination']
      }]
    override.ssh.username         = $configuration['override.ssh.username']
    override.ssh.private_key_path = $configuration['override.ssh.private_key_path']
  end
end  
