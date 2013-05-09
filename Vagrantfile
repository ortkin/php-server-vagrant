# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "precise32"
  config.vm.box_url = "http://files.vagrantup.com/precise32.box"
  config.vm.network :forwarded_port, guest: 80, host: 8080
  config.vm.network :private_network, ip: "192.168.33.10"

 # config.vm.synced_folder "../data", "/vagrant_data"
  config.vm.synced_folder "www","/var/www"

  config.vm.provision :chef_solo do |chef|
    chef.cookbooks_path = "cookbooks"

    chef.add_recipe "PHP_server"

    # You may also specify custom JSON attributes:
    chef.json = { 
      "apache" => {
        "listen_ports" => [ "80", "443" ],
        "default_site_enabled" => true
      },
      "mysql" => {
        "server_root_password" => "root",
        "server_repl_password" => "repl",
        "server_debian_password" => "debian"
      }
    }
  end
end
