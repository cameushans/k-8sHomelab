Vagrant.configure("2") do |config|

    NODES = [
        {hostname:"haproxy-1", ip:"192.168.50.10", type:"proxy"},
        {hostname:"master-1", ip:"192.168.50.12", type:"master"},
        {hostname:"worker-1", ip:"192.168.50.13", type:"worker"},
        {hostname:"worker-2", ip:"192.168.50.15", type:"worker"},
        {hostname:"worker-3", ip:"192.168.50.16", type:"worker"}
    ]

    box_centos = "generic/centos8"
    box_debian = "generic/debian11"

    NODES.each do |node|
        config.vm.network "private_network", ip: node[:ip]
        config.vm.define node[:hostname] do |cfg|
          cfg.vm.hostname = node[:hostname]
          if node[:type] != "proxy"
              cfg.vm.box = box_centos
              config.vm.provider :libvirt do |v|
                v.memory = 3000
              end
              cfg.vm.provision :shell do |shell|
                shell.path = "provisioning/containerRuntime"
              end
          else
              cfg.vm.box = box_debian
              cfg.vm.provision :shell do |shell|
                shell.path = "provisioning/haproxy"
              end
          end
        end
    end
end

