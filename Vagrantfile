# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
    boxes = [
        {
            :name => "ubuntu-bionic",
            :box => "ubuntu/bionic64",
            :host_vars => {
                "ansible_python_interpreter" => "/usr/bin/python3"
            }
        }
    ]
    host_vars = {}
    boxes.each do |opts|
        config.vm.define opts[:name] do |config|
            config.vm.box = opts[:box]
            host_vars[opts[:name]] = opts[:host_vars]
            if opts[:name] == boxes.last[:name]
                config.vm.provision "ansible" do |ansible|
                    ansible.playbook = "tests/playbook.yml"
                    ansible.limit = "all"
                    ansible.host_vars = host_vars
                end
            end
        end
    end
end
