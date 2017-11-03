Vagrant.configure("2") do |config|
  config.vbguest.auto_update = false
  
  config.vm.define "fedora" do |fedora|
    fedora.vm.box = "fedora/26-cloud-base"
    fedora.vm.provision "shell" do |s|
      s.inline = "dnf -y install python python2-dnf libselinux-python"
    end
    fedora.vm.synced_folder ".", "/vagrant", disabled: true
  end

  config.vm.define "centos" do |centos|
    centos.vm.box = "centos/7"
    centos.vm.provision "ansible" do |a|
      a.limit = "all"
      a.playbook = "tests/test.yml"
    end
    centos.vm.synced_folder ".", "/vagrant", disabled: true
  end
end
