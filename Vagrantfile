# -*- mode: ruby -*-
# vi: set ft=ruby :
#machines configuration 
machines = {
  "master" => {"memory" =>"512", "cpu" =>"1", "ip" =>"100", "image" => "bento/ubuntu-22.04"},
  "node01" => {"memory" =>"512", "cpu" =>"1", "ip" =>"101", "image" => "bento/ubuntu-22.04"},
  "node02" => {"memory" =>"512", "cpu" =>"1", "ip" =>"102", "image" => "bento/ubuntu-22.04"},
  "node03" => {"memory" =>"512", "cpu" =>"1", "ip" =>"103", "image" => "bento/ubuntu-22.04"}
}

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version.
Vagrant.configure("2") do |config|

  machines.each do |name, conf|
    config.vm.define "#{name}" do |machine|
      # Every Vagrant development environment requires a box.
      machine.vm.box = "#{conf["image"]}"
      machine.vm.hostname = "#{name}"
      # Create a private network, which allows host-only access to the machine
      # using a specific IP.
      machine.vm.network "private_network", ip: "10.10.10.#{conf["ip"]}"

        # These expose provider-specific options.
      machine.vm.provider "virtualbox" do |vb|
        vb.name ="#{name}"
        vb.memory = conf["memory"]
        vb.cpus = conf["cpu"]
      end

      # Enable provisioning with a shell script.
      config.vm.provision "shell", path:"docker.sh"
      if "#{name}" == "master"
        #Docker master provisioning
        machine.vm.provision "shell", path: "master.sh"
      else
        #Docker worker provisioning
        machine.vm.provision "shell", path: "worker.sh"
      end

    end
  end
end
