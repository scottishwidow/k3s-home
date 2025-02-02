Vagrant.configure("2") do |config|
  nodes = {
    "control-plane-1" => "192.168.56.11",
    "control-plane-2" => "192.168.56.12",
    "control-plane-3" => "192.168.56.13",
    "worker-1" => "192.168.56.21",
    "worker-2" => "192.168.56.22"
  }

  nodes.each do |hostname, ip|
    config.vm.define hostname do |node|
      node.vm.box = "debian/bookworm64"
      node.vm.hostname = hostname
      node.vm.network "private_network", ip: ip

      node.vm.provider "virtualbox" do |vb|
        vb.memory = "1024"
        vb.cpus = 1
        disk_path = File.expand_path("disk-#{hostname}.vdi", Dir.pwd) # Ensure full path

        # Check if disk already exists to prevent errors
        unless File.exist?(disk_path)
          vb.customize ["createhd", "--filename", disk_path, "--size", 20480]
        end

        vb.customize ["storageattach", :id, "--storagectl", "SATA Controller",
                      "--port", 1, "--device", 0, "--type", "hdd", "--medium", disk_path]
      end
    end
  end

  config.vm.post_up_message = "\nK3s Cluster Node IPs:\n" + nodes.map { |name, ip| "#{name}: #{ip}" }.join("\n")
end

