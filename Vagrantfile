REQUIRED_PLUGINS = %w(vagrant-libvirt)
exit unless REQUIRED_PLUGINS.all? do |plugin|
  Vagrant.has_plugin?(plugin) || (
    puts "The #{plugin} plugin is required. Please install it with:"
    puts "$ vagrant plugin install #{plugin}"
    false
  )
end

proxy_count = 1
manager_count = 1
worker_count = 1
machine_count = proxy_count + manager_count + worker_count

Vagrant.configure(2) do |config|
  # Enable use of single (insecure) SSH key to make testing easier.
  config.ssh.insert_key = false
  
  config.vm.box = "debian/bookworm64"

  (1..machine_count).each do |i|
    if i <= proxy_count
      name = "proxy-#{i}"
      config.vm.define name do |node|
        node.vm.hostname = name
        node.vm.network "private_network", type: "dhcp", ip: "10.10.10.#{i}0"
    
        config.vm.provider :libvirt do |libvirt|
          libvirt.cpus = 1
          libvirt.memory = 512
        end
      end
    elsif i <= proxy_count + manager_count
      name = "manager-#{i - proxy_count}"
      config.vm.define name do |node|
        node.vm.hostname = name
        node.vm.network "private_network", type: "dhcp", ip: "10.10.10.#{i}0"

        config.vm.provider :libvirt do |libvirt|
          libvirt.cpus = 1
          libvirt.memory = 1024
        end
      end
    else
      name = "worker-#{i - proxy_count - manager_count}"
      config.vm.define name do |node|
        node.vm.hostname = name
        node.vm.network "private_network", type: "dhcp", ip: "10.10.10.#{i}0"

        config.vm.provider :libvirt do |libvirt|
          libvirt.cpus = 1
          libvirt.memory = 1024
        end
      end
    end
  end
end