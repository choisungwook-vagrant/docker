require 'yaml'

CONFIG = YAML.load_file(File.join(File.dirname(__FILE__), 'config.yml'))

Vagrant.configure("2") do |config|
  config.ssh.insert_key = false

  config.vm.define CONFIG['server']['name'] do |cfg|
    cfg.vm.box = CONFIG['server']['box']
    cfg.vm.network "public_network", ip: CONFIG['server']['ip']
    cfg.vm.hostname = CONFIG['server']['hostname']
    
    cfg.vm.provider "virtualbox" do |v|
      v.memory = CONFIG['server']['memory']
      v.cpus = CONFIG['server']['cpu']
      v.name = CONFIG['server']['name']
    end

    # ssh 비밀번호인증 활성화
    cfg.vm.provision "shell", inline: <<-SCRIPT
      sed -i -e 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config
      systemctl restart sshd
    SCRIPT

    # install docker
    cfg.vm.provision "shell", inline: <<-SCRIPT
      yum install -y yum-utils vim net-tools tmux
      yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
      yum install docker-ce docker-ce-cli containerd.io docker-compose -y
      systemctl enable docker
      systemctl start docker
    SCRIPT
  end
end