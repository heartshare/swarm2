REQUIRED_PLUGINS = %w(vagrant-libvirt)
exit unless REQUIRED_PLUGINS.all? do |plugin|
  Vagrant.has_plugin?(plugin) || (
    puts "The #{plugin} plugin is required. Please install it with:"
    puts "$ vagrant plugin install #{plugin}"
    false
  )
end

manager_count = 2
worker_count = 1
machine_count = manager_count + worker_count

Vagrant.configure(2) do |config|
  config.vm.box = "debian/bookworm64"

  (1..machine_count).each do |i|
    if i <= manager_count
      config.vm.define "manager-#{i}" do |node|
        node.vm.hostname = "manager-#{i}"
        node.vm.network "private_network", type: "dhcp", ip: "10.10.10.#{i}0"

        config.vm.provider :libvirt do |libvirt|
          libvirt.cpus = 1
          libvirt.memory = 1024
        end
      end
    else
      config.vm.define "worker-#{i}" do |node|
        node.vm.hostname = "worker-#{i}"
        node.vm.network "private_network", type: "dhcp", ip: "10.10.10.#{i}0"

        config.vm.provider :libvirt do |libvirt|
          libvirt.cpus = 1
          libvirt.memory = 1024
        end
      end
    end
  end
end