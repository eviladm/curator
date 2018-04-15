Vagrant.configure("2") do |config|
config.vm.network "public_network", bridge: "en0: Wi-Fi (AirPort)"

  config.vm.define "centos" do |centos|
    centos.vm.box = "centos/7"
     centos.vm.provision "shell" do |s|
      ssh_pub_key = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip
      s.privileged = true
      s.inline = <<-SHELL
      [[ -d /root/.ssh ]] || mkdir /root/.ssh
      [[ $(grep skain ~/.ssh/authorized_keys 2> /dev/null) ]] || echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
      [[ $(grep skain /root/.ssh/authorized_keys 2> /dev/null) ]] || echo #{ssh_pub_key} >> /root/.ssh/authorized_keys
      SHELL
    end
    centos.vm.provision "ansible" do |ansible|
      ansible.playbook = "curator.yaml"
    end
  end

  config.vm.define "debian" do |debian|
    debian.vm.box = "debian/jessie64"
     debian.vm.provision "shell" do |s|
      ssh_pub_key = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip
      s.privileged = true
      s.inline = <<-SHELL
      [[ -d /root/.ssh ]] || mkdir /root/.ssh
      [[ $(grep skain ~/.ssh/authorized_keys 2> /dev/null) ]] || echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
      [[ $(grep skain /root/.ssh/authorized_keys 2> /dev/null) ]] || echo #{ssh_pub_key} >> /root/.ssh/authorized_keys
      SHELL
    end
     debian.vm.provision "ansible" do |ansible|
      ansible.playbook = "curator.yaml"
    end
 end
end
