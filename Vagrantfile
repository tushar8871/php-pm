Vagrant.configure("2") do |config|

  #using generated key not working
  config.ssh.insert_key = false
  # specs for all vms
  config.vm.provider "virtualbox" do |v|
    v.memory = 2048
    v.cpus = 2
  end

  config.vm.define "php" do |php|
    php.vm.box = "laravel/homestead-7"
    php.vm.box_version = "0.2.1"
    php.vm.hostname = 'php'
  end
end
