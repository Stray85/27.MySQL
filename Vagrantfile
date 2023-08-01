Vagrant.configure(2) do |config|
config.vm.box = "centos/7"


	config.vm.define "master" do |master|
	master.vm.hostname = "master"
	master.vm.network "private_network", ip: "192.168.56.10"
	config.vm.provision "shell", inline: <<-SHELL
	sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config
	systemctl restart sshd
	echo vagrant | passwd vagrant --stdin
	yum install -y https://repo.percona.com/yum/percona-release-latest.noarch.rpm
    yum install -y Percona-Server-server-57
	yum install nano
	cp /vagrant/conf/conf.d.master/* /etc/my.cnf.d/
	systemctl start mysqld
	SHELL
	end


	config.vm.define "slave" do |slave|
	slave.vm.hostname = "slave"
	slave.vm.network "private_network", ip: "192.168.56.20"
	config.vm.provision "shell", inline: <<-SHELL
	sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config
	systemctl restart sshd
	echo vagrant | passwd vagrant --stdin
	yum install -y https://repo.percona.com/yum/percona-release-latest.noarch.rpm
    yum install -y Percona-Server-server-57
	yum install nano
	cp /vagrant/conf/conf.d.slave/* /etc/my.cnf.d/
	systemctl start mysqld
	SHELL
	end
	
end