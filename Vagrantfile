Vagrant.configure("2") do |vcfg|
  (1..4).each{|i|
		name = "db#{i}".to_sym()
		vcfg.vm.define name do |config|
			# Change this to centos-64-x64 if you downloaded the 64-bit image
			config.vm.box = "centos-64-i386"
			
			config.vm.provider :virtualbox do |vb|
				# Update this line to increase the amount of available memory
        vb.customize ["modifyvm", :id, "--memory", "1024"]
      end

			config.vm.hostname = "db#{i}"
      config.vm.network "private_network", :ip => "192.168.11.10#{i}"

			config.vm.provision "puppet" do |puppet|
        puppet.options = ""
        puppet.module_path = "modules"
        puppet.facter = {
          "vagrant" => "1",
          "fqdn" => "db#{i}"
        }
      end
		end
	}
end