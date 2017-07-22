Vagrant.configure("2") do |config|
  
config.vm.define "ubuntu1" do |ubuntu1|  
  ubuntu1.vm.box = "ubuntu/trusty64"
  ubuntu1.vm.hostname = "ubuntu1"
  ubuntu1.vm.network "forwarded_port", guest: 22, host: 2222, id: "ssh", disabled: true
  ubuntu1.vm.network "forwarded_port", guest: 22, host: 1001
  ubuntu1.vm.network :private_network, ip: "100.1.1.1/24"
  ubuntu1.vm.network :private_network, ip: "100.2.2.1/24"
  ubuntu1.vm.network :private_network, ip: "101.101.101.1/24"
  ubuntu1.vm.provision "shell", inline: "sudo chmod 777 /etc/sysctl.d"
  ubuntu1.vm.provision "file", source: "./99quagga_defaults.conf", destination: "/etc/sysctl.d/99quagga_defaults.conf"
  ubuntu1.vm.provision "shell", inline: "wget http://cumulusfiles.s3.amazonaws.com/roh-3.3.0-ubuntu1404.tar"#pull down cumulus roh image - issues w/ vpn and dns
  ubuntu1.vm.provision "shell", inline: "tar xvf roh-3.3.0-ubuntu1404.tar"#untar and install - note package version and ubuntu version
  ubuntu1.vm.provision "shell", inline: "sudo dpkg -i quagga_1.0.0+cl3u11-0~ubuntu14.04+1~1493952436.3ae65f1_amd64.deb quagga-dbg_1.0.0+cl3u11-0~ubuntu14.04+1~1493952436.3ae65f1_amd64.deb quagga-doc_1.0.0+cl3u11-0~ubuntu14.04+1~1493952436.3ae65f1_all.deb"
  ubuntu1.vm.provision "shell", inline: "sed -i 's/zebra=no/zebra=yes/g' /etc/quagga/daemons"
  ubuntu1.vm.provision "shell", inline: "sed -i 's/bgpd=no/bgpd=yes/g' /etc/quagga/daemons"
  ubuntu1.vm.provision "shell", inline: "sudo service quagga restart"
  ubuntu1.vm.provision "shell", inline: "sleep 5"
  ubuntu1.vm.provision "shell", inline: "sudo apt-mark hold quagga"
  ubuntu1.vm.provision "shell", inline: "echo 'router bgp 65501' |  sudo tee -a /etc/quagga/Quagga.conf"
  ubuntu1.vm.provision "shell", inline: "echo 'bgp bestpath as-path multipath-relax' |  sudo tee -a /etc/quagga/Quagga.conf"
  ubuntu1.vm.provision "shell", inline: "echo 'neighbor ToR peer-group' |  sudo tee -a /etc/quagga/Quagga.conf"
  ubuntu1.vm.provision "shell", inline: "echo 'neighbor ToR remote-as external' |  sudo tee -a /etc/quagga/Quagga.conf"
  ubuntu1.vm.provision "shell", inline: "echo 'neighbor eth1 interface peer-group ToR' |  sudo tee -a /etc/quagga/Quagga.conf"
  ubuntu1.vm.provision "shell", inline: "echo 'neighbor eth2 interface peer-group ToR' |  sudo tee -a /etc/quagga/Quagga.conf"
  ubuntu1.vm.provision "shell", inline: "echo 'network 101.101.101.0 mask 255.255.255.0' |  sudo tee -a /etc/quagga/Quagga.conf"#ubuntu1 host network
  ubuntu1.vm.provision "shell", inline: "echo 'no neighbor ToR capability extended-nexthop' |  sudo tee -a /etc/quagga/Quagga.conf"
  ubuntu1.vm.provision "shell", inline: "echo 'log file /var/log/quagga/quagga.log' |  sudo tee -a /etc/quagga/Quagga.conf"
  ubuntu1.vm.provision "shell", inline: "sudo sysctl -p /etc/sysctl.d/"
  ubuntu1.vm.provision "shell", inline: "sudo service quagga restart"

  end

config.vm.define "ubuntu2" do |ubuntu2|  
  ubuntu2.vm.box = "ubuntu/trusty64"
  ubuntu2.vm.hostname = "ubuntu2"
  ubuntu2.vm.network "forwarded_port", guest: 22, host: 2222, id: "ssh", disabled: true
  ubuntu2.vm.network "forwarded_port", guest: 22, host: 1002
  ubuntu2.vm.network :private_network, ip: "100.3.3.1/24"
  ubuntu2.vm.network :private_network, ip: "100.4.4.1/24"
  ubuntu2.vm.network :private_network, ip: "102.102.102.1/24"
  ubuntu2.vm.provision "shell", inline: "sudo chmod 777 /etc/sysctl.d"
  ubuntu2.vm.provision "file", source: "./99quagga_defaults.conf", destination: "/etc/sysctl.d/99quagga_defaults.conf"
  ubuntu2.vm.provision "shell", inline: "wget http://cumulusfiles.s3.amazonaws.com/roh-3.3.0-ubuntu1404.tar"#pull down cumulus roh image - issues w/ vpn and dns
  ubuntu2.vm.provision "shell", inline: "tar xvf roh-3.3.0-ubuntu1404.tar"#untar and install - note package version and ubuntu version
  ubuntu2.vm.provision "shell", inline: "sudo dpkg -i quagga_1.0.0+cl3u11-0~ubuntu14.04+1~1493952436.3ae65f1_amd64.deb quagga-dbg_1.0.0+cl3u11-0~ubuntu14.04+1~1493952436.3ae65f1_amd64.deb quagga-doc_1.0.0+cl3u11-0~ubuntu14.04+1~1493952436.3ae65f1_all.deb"
  ubuntu2.vm.provision "shell", inline: "sed -i 's/zebra=no/zebra=yes/g' /etc/quagga/daemons"
  ubuntu2.vm.provision "shell", inline: "sed -i 's/bgpd=no/bgpd=yes/g' /etc/quagga/daemons"
  ubuntu2.vm.provision "shell", inline: "sudo service quagga restart"
  ubuntu2.vm.provision "shell", inline: "sleep 5"
  ubuntu2.vm.provision "shell", inline: "sudo apt-mark hold quagga"
  ubuntu2.vm.provision "shell", inline: "echo 'router bgp 65502' |  sudo tee -a /etc/quagga/Quagga.conf"
  ubuntu2.vm.provision "shell", inline: "echo 'bgp bestpath as-path multipath-relax' |  sudo tee -a /etc/quagga/Quagga.conf"
  ubuntu2.vm.provision "shell", inline: "echo 'neighbor ToR peer-group' |  sudo tee -a /etc/quagga/Quagga.conf"
  ubuntu2.vm.provision "shell", inline: "echo 'neighbor ToR remote-as external' |  sudo tee -a /etc/quagga/Quagga.conf"
  ubuntu2.vm.provision "shell", inline: "echo 'neighbor eth1 interface peer-group ToR' |  sudo tee -a /etc/quagga/Quagga.conf"
  ubuntu2.vm.provision "shell", inline: "echo 'neighbor eth2 interface peer-group ToR' |  sudo tee -a /etc/quagga/Quagga.conf"
  ubuntu2.vm.provision "shell", inline: "echo 'network 102.102.102.0 mask 255.255.255.0' |  sudo tee -a /etc/quagga/Quagga.conf"#ubuntu2 host network
  ubuntu2.vm.provision "shell", inline: "echo 'no neighbor ToR capability extended-nexthop' |  sudo tee -a /etc/quagga/Quagga.conf"
  ubuntu2.vm.provision "shell", inline: "echo 'log file /var/log/quagga/quagga.log' |  sudo tee -a /etc/quagga/Quagga.conf"
  ubuntu2.vm.provision "shell", inline: "sudo sysctl -p /etc/sysctl.d/"
  ubuntu2.vm.provision "shell", inline: "sudo service quagga restart"

  end

config.vm.define "leaf1" do |leaf1|  
  leaf1.vm.box = "CumulusCommunity/cumulus-vx"
  leaf1.vm.network :private_network, ip: "10.10.1.0/31"
  leaf1.vm.network :private_network, ip: "10.10.2.0/31"
  leaf1.vm.network :private_network, ip: "100.1.1.2/24"#link to ubuntu1
  leaf1.vm.network :private_network, ip: "1.1.1.1/32"
  leaf1.vm.hostname = "leaf1"
  leaf1.vm.network "forwarded_port", guest: 22, host: 2222, id: "ssh", disabled: true
  leaf1.vm.network "forwarded_port", guest: 22, host: 2001
  leaf1.vm.provision "shell", inline: "sed -i 's/zebra=no/zebra=yes/g' /etc/quagga/daemons"
  leaf1.vm.provision "shell", inline: "sed -i 's/bgpd=no/bgpd=yes/g' /etc/quagga/daemons"
  leaf1.vm.provision "shell", inline: "sudo systemctl restart quagga.service"
  leaf1.vm.provision "shell", inline: "sleep 5"
  leaf1.vm.provision "shell", inline: "echo 'ip prefix-list DEFAULT_ONLY seq 5 permit 0.0.0.0/0' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf1.vm.provision "shell", inline: "echo 'ip as-path access-list 1 permit ^65501$' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf1.vm.provision "shell", inline: "echo 'route-map ROUTES_IN permit 10' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf1.vm.provision "shell", inline: "echo 'match as-path 1' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf1.vm.provision "shell", inline: "echo 'route-map ROUTES_OUT permit 10' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf1.vm.provision "shell", inline: "echo 'match ip address prefix-list DEFAULT_ONLY' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf1.vm.provision "shell", inline: "echo 'router bgp 65101' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf1.vm.provision "shell", inline: "echo 'bgp router-id 1.1.1.1' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf1.vm.provision "shell", inline: "echo 'bgp bestpath as-path multipath-relax' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf1.vm.provision "shell", inline: "echo 'neighbor EBGP peer-group' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf1.vm.provision "shell", inline: "echo 'neighbor EBGP remote-as external' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf1.vm.provision "shell", inline: "echo 'neighbor swp1 interface peer-group EBGP' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf1.vm.provision "shell", inline: "echo 'neighbor swp2 interface peer-group EBGP' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf1.vm.provision "shell", inline: "echo 'network 1.1.1.1 mask 255.255.255.255' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf1.vm.provision "shell", inline: "echo 'network 10.10.1.0 mask 255.255.255.254' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf1.vm.provision "shell", inline: "echo 'network 10.10.2.0 mask 255.255.255.254' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf1.vm.provision "shell", inline: "echo 'no neighbor EBGP capability extended-nexthop' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf1.vm.provision "shell", inline: "echo 'neighbor SRVR peer-group' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf1.vm.provision "shell", inline: "echo 'neighbor SRVR remote-as external' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf1.vm.provision "shell", inline: "echo 'neighbor SRVR default-originate' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf1.vm.provision "shell", inline: "echo 'neighbor SRVR maximum-prefix 10' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf1.vm.provision "shell", inline: "echo 'neighbor SRVR route-map ROUTES_IN in' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf1.vm.provision "shell", inline: "echo 'neighbor SRVR route-map ROUTES_OUT out' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf1.vm.provision "shell", inline: "echo 'neighbor swp3 interface peer-group SRVR' |  sudo tee -a /etc/quagga/Quagga.conf"#link to ubuntu1
  leaf1.vm.provision "shell", inline: "echo 'network 100.1.1.0 mask 255.255.255.0' |  sudo tee -a /etc/quagga/Quagga.conf"#link to ubuntu1
  leaf1.vm.provision "shell", inline: "echo 'no neighbor SRVR capability extended-nexthop' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf1.vm.provision "shell", inline: "echo 'log file /var/log/quagga/quagga.log' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf1.vm.provision "shell", inline: "sudo systemctl restart quagga.service"

  end

config.vm.define "leaf2" do |leaf2|  
  leaf2.vm.box = "CumulusCommunity/cumulus-vx"
  leaf2.vm.network :private_network, ip: "20.20.1.0/31"
  leaf2.vm.network :private_network, ip: "20.20.2.0/31"
  leaf2.vm.network :private_network, ip: "100.2.2.2/24"#link to ubuntu1
  leaf2.vm.network :private_network, ip: "2.2.2.2/32"
  leaf2.vm.hostname = "leaf2"
  leaf2.vm.network "forwarded_port", guest: 22, host: 2222, id: "ssh", disabled: true
  leaf2.vm.network "forwarded_port", guest: 22, host: 2002
  leaf2.vm.provision "shell", inline: "sed -i 's/zebra=no/zebra=yes/g' /etc/quagga/daemons"
  leaf2.vm.provision "shell", inline: "sed -i 's/bgpd=no/bgpd=yes/g' /etc/quagga/daemons"
  leaf2.vm.provision "shell", inline: "sudo systemctl restart quagga.service"
  leaf2.vm.provision "shell", inline: "sleep 5"
  leaf2.vm.provision "shell", inline: "echo 'ip prefix-list DEFAULT_ONLY seq 5 permit 0.0.0.0/0' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf2.vm.provision "shell", inline: "echo 'ip as-path access-list 1 permit ^65501$' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf2.vm.provision "shell", inline: "echo 'route-map ROUTES_IN permit 10' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf2.vm.provision "shell", inline: "echo 'match as-path 1' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf2.vm.provision "shell", inline: "echo 'route-map ROUTES_OUT permit 10' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf2.vm.provision "shell", inline: "echo 'match ip address prefix-list DEFAULT_ONLY' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf2.vm.provision "shell", inline: "echo 'router bgp 65102' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf2.vm.provision "shell", inline: "echo 'bgp router-id 2.2.2.2' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf2.vm.provision "shell", inline: "echo 'bgp bestpath as-path multipath-relax' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf2.vm.provision "shell", inline: "echo 'neighbor EBGP peer-group' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf2.vm.provision "shell", inline: "echo 'neighbor EBGP remote-as external' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf2.vm.provision "shell", inline: "echo 'neighbor swp1 interface peer-group EBGP' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf2.vm.provision "shell", inline: "echo 'neighbor swp2 interface peer-group EBGP' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf2.vm.provision "shell", inline: "echo 'network 2.2.2.2 mask 255.255.255.255' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf2.vm.provision "shell", inline: "echo 'network 20.20.1.0 mask 255.255.255.254' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf2.vm.provision "shell", inline: "echo 'network 20.20.2.0 mask 255.255.255.254' |  sudo tee -a /etc/quagga/Quagga.conf"  
  leaf2.vm.provision "shell", inline: "echo 'no neighbor EBGP capability extended-nexthop' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf2.vm.provision "shell", inline: "echo 'neighbor SRVR peer-group' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf2.vm.provision "shell", inline: "echo 'neighbor SRVR remote-as external' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf2.vm.provision "shell", inline: "echo 'neighbor SRVR default-originate' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf2.vm.provision "shell", inline: "echo 'neighbor SRVR maximum-prefix 10' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf2.vm.provision "shell", inline: "echo 'neighbor SRVR route-map ROUTES_IN in' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf2.vm.provision "shell", inline: "echo 'neighbor SRVR route-map ROUTES_OUT out' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf2.vm.provision "shell", inline: "echo 'neighbor swp3 interface peer-group SRVR' |  sudo tee -a /etc/quagga/Quagga.conf"#link to ubuntu1
  leaf2.vm.provision "shell", inline: "echo 'network 100.2.2.0 mask 255.255.255.0' |  sudo tee -a /etc/quagga/Quagga.conf"#link to ubuntu1
  leaf2.vm.provision "shell", inline: "echo 'no neighbor SRVR capability extended-nexthop' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf2.vm.provision "shell", inline: "echo 'log file /var/log/quagga/quagga.log' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf2.vm.provision "shell", inline: "sudo systemctl restart quagga.service"
  
  end

config.vm.define "leaf3" do |leaf3|  
  leaf3.vm.box = "CumulusCommunity/cumulus-vx"
  leaf3.vm.network :private_network, ip: "30.30.1.0/31"
  leaf3.vm.network :private_network, ip: "30.30.2.0/31"
  leaf3.vm.network :private_network, ip: "100.3.3.2/24"#link to ubuntu2
  leaf3.vm.network :private_network, ip: "3.3.3.3/32"
  leaf3.vm.hostname = "leaf3"
  leaf3.vm.network "forwarded_port", guest: 22, host: 2222, id: "ssh", disabled: true
  leaf3.vm.network "forwarded_port", guest: 22, host: 2003
  leaf3.vm.provision "shell", inline: "sed -i 's/zebra=no/zebra=yes/g' /etc/quagga/daemons"
  leaf3.vm.provision "shell", inline: "sed -i 's/bgpd=no/bgpd=yes/g' /etc/quagga/daemons"
  leaf3.vm.provision "shell", inline: "sudo systemctl restart quagga.service"
  leaf3.vm.provision "shell", inline: "sleep 5"
  leaf3.vm.provision "shell", inline: "echo 'ip prefix-list DEFAULT_ONLY seq 5 permit 0.0.0.0/0' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf3.vm.provision "shell", inline: "echo 'ip as-path access-list 1 permit ^65502$' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf3.vm.provision "shell", inline: "echo 'route-map ROUTES_IN permit 10' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf3.vm.provision "shell", inline: "echo 'match as-path 1' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf3.vm.provision "shell", inline: "echo 'route-map ROUTES_OUT permit 10' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf3.vm.provision "shell", inline: "echo 'match ip address prefix-list DEFAULT_ONLY' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf3.vm.provision "shell", inline: "echo 'router bgp 65103' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf3.vm.provision "shell", inline: "echo 'bgp router-id 3.3.3.3' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf3.vm.provision "shell", inline: "echo 'bgp bestpath as-path multipath-relax' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf3.vm.provision "shell", inline: "echo 'neighbor EBGP peer-group' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf3.vm.provision "shell", inline: "echo 'neighbor EBGP remote-as external' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf3.vm.provision "shell", inline: "echo 'neighbor swp1 interface peer-group EBGP' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf3.vm.provision "shell", inline: "echo 'neighbor swp2 interface peer-group EBGP' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf3.vm.provision "shell", inline: "echo 'network 3.3.3.3 mask 255.255.255.255' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf3.vm.provision "shell", inline: "echo 'network 30.30.1.0 mask 255.255.255.254' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf3.vm.provision "shell", inline: "echo 'network 30.30.2.0 mask 255.255.255.254' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf3.vm.provision "shell", inline: "echo 'no neighbor EBGP capability extended-nexthop' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf3.vm.provision "shell", inline: "echo 'neighbor SRVR peer-group' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf3.vm.provision "shell", inline: "echo 'neighbor SRVR remote-as external' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf3.vm.provision "shell", inline: "echo 'neighbor SRVR default-originate' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf3.vm.provision "shell", inline: "echo 'neighbor SRVR maximum-prefix 10' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf3.vm.provision "shell", inline: "echo 'neighbor SRVR route-map ROUTES_IN in' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf3.vm.provision "shell", inline: "echo 'neighbor SRVR route-map ROUTES_OUT out' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf3.vm.provision "shell", inline: "echo 'neighbor swp3 interface peer-group SRVR' |  sudo tee -a /etc/quagga/Quagga.conf"#link to ubuntu2
  leaf3.vm.provision "shell", inline: "echo 'network 100.3.3.0 mask 255.255.255.0' |  sudo tee -a /etc/quagga/Quagga.conf"#link to ubuntu2
  leaf3.vm.provision "shell", inline: "echo 'no neighbor SRVR capability extended-nexthop' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf3.vm.provision "shell", inline: "echo 'log file /var/log/quagga/quagga.log' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf3.vm.provision "shell", inline: "sudo systemctl restart quagga.service"
  
  end

config.vm.define "leaf4" do |leaf4|  
  leaf4.vm.box = "CumulusCommunity/cumulus-vx"
  leaf4.vm.network :private_network, ip: "40.40.1.0/31"
  leaf4.vm.network :private_network, ip: "40.40.2.0/31"
  leaf4.vm.network :private_network, ip: "100.4.4.2/24"#link to ubuntu2
  leaf4.vm.network :private_network, ip: "4.4.4.4/32"
  leaf4.vm.hostname = "leaf4"
  leaf4.vm.network "forwarded_port", guest: 22, host: 2222, id: "ssh", disabled: true
  leaf4.vm.network "forwarded_port", guest: 22, host: 2004
  leaf4.vm.provision "shell", inline: "sed -i 's/zebra=no/zebra=yes/g' /etc/quagga/daemons"
  leaf4.vm.provision "shell", inline: "sed -i 's/bgpd=no/bgpd=yes/g' /etc/quagga/daemons"
  leaf4.vm.provision "shell", inline: "sudo systemctl restart quagga.service"
  leaf4.vm.provision "shell", inline: "sleep 5"
  leaf4.vm.provision "shell", inline: "echo 'ip prefix-list DEFAULT_ONLY seq 5 permit 0.0.0.0/0' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf4.vm.provision "shell", inline: "echo 'ip as-path access-list 1 permit ^65502$' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf4.vm.provision "shell", inline: "echo 'route-map ROUTES_IN permit 10' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf4.vm.provision "shell", inline: "echo 'match as-path 1' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf4.vm.provision "shell", inline: "echo 'route-map ROUTES_OUT permit 10' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf4.vm.provision "shell", inline: "echo 'match ip address prefix-list DEFAULT_ONLY' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf4.vm.provision "shell", inline: "echo 'router bgp 65104' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf4.vm.provision "shell", inline: "echo 'bgp router-id 4.4.4.4' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf4.vm.provision "shell", inline: "echo 'bgp bestpath as-path multipath-relax' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf4.vm.provision "shell", inline: "echo 'neighbor EBGP peer-group' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf4.vm.provision "shell", inline: "echo 'neighbor EBGP remote-as external' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf4.vm.provision "shell", inline: "echo 'neighbor swp1 interface peer-group EBGP' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf4.vm.provision "shell", inline: "echo 'neighbor swp2 interface peer-group EBGP' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf4.vm.provision "shell", inline: "echo 'network 4.4.4.4 mask 255.255.255.255' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf4.vm.provision "shell", inline: "echo 'network 40.40.1.0 mask 255.255.255.254' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf4.vm.provision "shell", inline: "echo 'network 40.40.2.0 mask 255.255.255.254' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf4.vm.provision "shell", inline: "echo 'no neighbor EBGP capability extended-nexthop' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf4.vm.provision "shell", inline: "echo 'neighbor SRVR peer-group' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf4.vm.provision "shell", inline: "echo 'neighbor SRVR remote-as external' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf4.vm.provision "shell", inline: "echo 'neighbor SRVR default-originate' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf4.vm.provision "shell", inline: "echo 'neighbor SRVR maximum-prefix 10' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf4.vm.provision "shell", inline: "echo 'neighbor SRVR route-map ROUTES_IN in' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf4.vm.provision "shell", inline: "echo 'neighbor SRVR route-map ROUTES_OUT out' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf4.vm.provision "shell", inline: "echo 'neighbor swp3 interface peer-group SRVR' |  sudo tee -a /etc/quagga/Quagga.conf"#link to ubuntu2
  leaf4.vm.provision "shell", inline: "echo 'network 100.4.4.0 mask 255.255.255.0' |  sudo tee -a /etc/quagga/Quagga.conf"#link to ubuntu2
  leaf4.vm.provision "shell", inline: "echo 'no neighbor SRVR capability extended-nexthop' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf4.vm.provision "shell", inline: "echo 'log file /var/log/quagga/quagga.log' |  sudo tee -a /etc/quagga/Quagga.conf"
  leaf4.vm.provision "shell", inline: "sudo systemctl restart quagga.service"
  
  end
  
config.vm.define "spine1" do |spine1|  
  spine1.vm.box = "CumulusCommunity/cumulus-vx"
  spine1.vm.network :private_network, ip: "10.10.1.1/31"
  spine1.vm.network :private_network, ip: "20.20.1.1/31"
  spine1.vm.network :private_network, ip: "30.30.1.1/31"
  spine1.vm.network :private_network, ip: "40.40.1.1/31"
  spine1.vm.network :private_network, ip: "11.11.11.11/32"
  spine1.vm.hostname = "spine1"
  spine1.vm.network "forwarded_port", guest: 22, host: 2222, id: "ssh", disabled: true
  spine1.vm.network "forwarded_port", guest: 22, host: 3001
  spine1.vm.provision "shell", inline: "sed -i 's/zebra=no/zebra=yes/g' /etc/quagga/daemons"
  spine1.vm.provision "shell", inline: "sed -i 's/bgpd=no/bgpd=yes/g' /etc/quagga/daemons"
  spine1.vm.provision "shell", inline: "sudo systemctl restart quagga.service"
  spine1.vm.provision "shell", inline: "sleep 5"
  spine1.vm.provision "shell", inline: "echo 'router bgp 65500' |  sudo tee -a /etc/quagga/Quagga.conf"
  spine1.vm.provision "shell", inline: "echo 'bgp router-id 11.11.11.11' |  sudo tee -a /etc/quagga/Quagga.conf"
  spine1.vm.provision "shell", inline: "echo 'bgp bestpath as-path multipath-relax' |  sudo tee -a /etc/quagga/Quagga.conf"
  spine1.vm.provision "shell", inline: "echo 'neighbor EBGP peer-group' |  sudo tee -a /etc/quagga/Quagga.conf"
  spine1.vm.provision "shell", inline: "echo 'neighbor EBGP remote-as external' |  sudo tee -a /etc/quagga/Quagga.conf"
  spine1.vm.provision "shell", inline: "echo 'neighbor swp1 interface peer-group EBGP' |  sudo tee -a /etc/quagga/Quagga.conf"
  spine1.vm.provision "shell", inline: "echo 'neighbor swp2 interface peer-group EBGP' |  sudo tee -a /etc/quagga/Quagga.conf"
  spine1.vm.provision "shell", inline: "echo 'neighbor swp3 interface peer-group EBGP' |  sudo tee -a /etc/quagga/Quagga.conf"
  spine1.vm.provision "shell", inline: "echo 'neighbor swp4 interface peer-group EBGP' |  sudo tee -a /etc/quagga/Quagga.conf"
  spine1.vm.provision "shell", inline: "echo 'network 11.11.11.11 mask 255.255.255.255' |  sudo tee -a /etc/quagga/Quagga.conf"
  spine1.vm.provision "shell", inline: "echo 'log file /var/log/quagga/quagga.log' |  sudo tee -a /etc/quagga/Quagga.conf"
  spine1.vm.provision "shell", inline: "sudo systemctl restart quagga.service"
  
  end

config.vm.define "spine2" do |spine2|  
  spine2.vm.box = "CumulusCommunity/cumulus-vx"
  spine2.vm.network :private_network, ip: "10.10.2.1/31"
  spine2.vm.network :private_network, ip: "20.20.2.1/31"
  spine2.vm.network :private_network, ip: "30.30.2.1/31"
  spine2.vm.network :private_network, ip: "40.40.2.1/31"
  spine2.vm.network :private_network, ip: "22.22.22.22/32"
  spine2.vm.hostname = "spine2"
  spine2.vm.network "forwarded_port", guest: 22, host: 2222, id: "ssh", disabled: true
  spine2.vm.network "forwarded_port", guest: 22, host: 3002
  spine2.vm.provision "shell", inline: "sed -i 's/zebra=no/zebra=yes/g' /etc/quagga/daemons"
  spine2.vm.provision "shell", inline: "sed -i 's/bgpd=no/bgpd=yes/g' /etc/quagga/daemons"
  spine2.vm.provision "shell", inline: "sudo systemctl restart quagga.service"
  spine2.vm.provision "shell", inline: "sleep 5"
  spine2.vm.provision "shell", inline: "echo 'router bgp 65500' |  sudo tee -a /etc/quagga/Quagga.conf"
  spine2.vm.provision "shell", inline: "echo 'bgp router-id 22.22.22.22' |  sudo tee -a /etc/quagga/Quagga.conf"
  spine2.vm.provision "shell", inline: "echo 'bgp bestpath as-path multipath-relax' |  sudo tee -a /etc/quagga/Quagga.conf"
  spine2.vm.provision "shell", inline: "echo 'neighbor EBGP peer-group' |  sudo tee -a /etc/quagga/Quagga.conf"
  spine2.vm.provision "shell", inline: "echo 'neighbor EBGP remote-as external' |  sudo tee -a /etc/quagga/Quagga.conf"
  spine2.vm.provision "shell", inline: "echo 'neighbor swp1 interface peer-group EBGP' |  sudo tee -a /etc/quagga/Quagga.conf"
  spine2.vm.provision "shell", inline: "echo 'neighbor swp2 interface peer-group EBGP' |  sudo tee -a /etc/quagga/Quagga.conf"
  spine2.vm.provision "shell", inline: "echo 'neighbor swp3 interface peer-group EBGP' |  sudo tee -a /etc/quagga/Quagga.conf"
  spine2.vm.provision "shell", inline: "echo 'neighbor swp4 interface peer-group EBGP' |  sudo tee -a /etc/quagga/Quagga.conf"
  spine2.vm.provision "shell", inline: "echo 'network 22.22.22.22 mask 255.255.255.255' |  sudo tee -a /etc/quagga/Quagga.conf"
  spine2.vm.provision "shell", inline: "echo 'log file /var/log/quagga/quagga.log' |  sudo tee -a /etc/quagga/Quagga.conf"
  spine2.vm.provision "shell", inline: "sudo systemctl restart quagga.service"
  
  end

end