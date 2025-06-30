Vagrant.configure("2") do |config|

  config.vm.define "vmubuntu" do |ubuntu|
    ubuntu.vm.box = "ubuntu/focal64"
    ubuntu.vm.hostname = "vmubuntu"
    ubuntu.vm.network "private_network", ip: "192.168.56.10"
    ubuntu.vm.provider "virtualbox" do |vb|
      vb.name = "VM_Ubuntu"
      vb.memory = 1024
      vb.cpus = 1
    end
    ubuntu.vm.disk :disk, size: "5GB", name: "disk1"
    ubuntu.vm.disk :disk, size: "3GB", name: "disk2"
    ubuntu.vm.disk :disk, size: "2GB", name: "disk3"
    ubuntu.vm.disk :disk, size: "1GB", name: "disk_extra"
  end

  config.vm.define "vmfedora" do |fedora|
    fedora.vm.box = "fedora/39-cloud-base"
    fedora.vm.hostname = "vmfedora"
    fedora.vm.network "private_network", ip: "192.168.56.101"
    fedora.vm.provider "virtualbox" do |vb|
      vb.name = "VM_Fedora"
      vb.memory = 1024
      vb.cpus = 1

      # Agregar un nuevo controlador SATA para discos extra
      vb.customize ['storagectl', :id, '--name', 'SATA Controller', '--add', 'sata', '--controller', 'IntelAHCI']
      vb.customize ['createhd', '--filename', 'disk1.vdi', '--size', 5120]
      vb.customize ['createhd', '--filename', 'disk2.vdi', '--size', 3072]
      vb.customize ['createhd', '--filename', 'disk3.vdi', '--size', 2048]
      vb.customize ['createhd', '--filename', 'disk_extra.vdi', '--size', 1024]
      vb.customize ['storageattach', :id, '--storagectl', 'SATA Controller', '--port', 1, '--device', 0, '--type', 'hdd', '--medium', 'disk1.vdi']
      vb.customize ['storageattach', :id, '--storagectl', 'SATA Controller', '--port', 2, '--device', 0, '--type', 'hdd', '--medium', 'disk2.vdi']
      vb.customize ['storageattach', :id, '--storagectl', 'SATA Controller', '--port', 3, '--device', 0, '--type', 'hdd', '--medium', 'disk3.vdi']
      vb.customize ['storageattach', :id, '--storagectl', 'SATA Controller', '--port', 4, '--device', 0, '--type', 'hdd', '--medium', 'disk_extra.vdi']
    end
  end

end
