Vagrant.configure("2") do |config|
  nodes = {
    "load-balancer-1" => "192.168.1.10",
    "control-plane-1" => "192.168.1.50",
    "control-plane-2" => "192.168.1.51",
    "worker-1" => "192.168.1.60",
    "worker-2" => "192.168.1.61"
  }

  nodes.each do |hostname, ip|
    config.vm.define hostname do |node|
      node.vm.box = "debian/bookworm64"
      node.vm.hostname = hostname
      node.vm.network "private_network", ip: ip

      node.vm.provider "virtualbox" do |vb|
        vb.memory = "1024"
        vb.cpus = 1
        disk_path = File.expand_path("disk-#{hostname}.vdi", Dir.pwd)

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

