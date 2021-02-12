Vagrant.configure('2') do |config|
  config.vm.define 'dev' do |config|
    config.vm.provider :digital_ocean do |provider, override|
      override.ssh.private_key_path = '~/.ssh/digital_ocean_rsa'
      override.vm.box = 'digital_ocean'
      override.vm.box_url = 'https://github.com/devopsgroup-io/vagrant-digitalocean/raw/master/box/digital_ocean.box'
      override.nfs.functional = false
      override.vm.allowed_synced_folder_types = :rsync
      if ENV['DIGITAL_OCEAN_TOKEN']
        provider.token = ENV['DIGITAL_OCEAN_TOKEN']
      else
        raise(Exception, "undefined variable: DIGITAL_OCEAN_TOKEN")
      end

      provider.image = 'ubuntu-20-04-x64'
      provider.region = 'nyc1'
      provider.size = 's-2vcpu-2gb'
      provider.backups_enabled = false
      provider.private_networking = false
      provider.ipv6 = false
      provider.monitoring = false
    end

    config.vm.provision :ansible do |ansible|
      ansible.playbook = 'playbook.yml'
    end
  end
end
