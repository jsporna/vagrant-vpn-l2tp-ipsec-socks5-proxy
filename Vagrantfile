Vagrant.configure("2") do |config|
    config.env.enable
    config.vm.box = "bento/ubuntu-20.04"
    config.vm.network "forwarded_port", guest: 1080, host: ENV['VPN_SOCKS_PORT']
    config.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbook.yml"
      ansible.extra_vars = {
        vpn_gateway: ENV['VPN_GATEWAY'],
        vpn_ipsec_psk: ENV['VPN_IPSEC_PSK'],
        vpn_user: ENV['VPN_USER'],
        vpn_password: ENV['VPN_PASSWORD']
      }
    end
  end
  