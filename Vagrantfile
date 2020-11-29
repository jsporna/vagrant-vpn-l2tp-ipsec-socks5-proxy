Vagrant.configure("2") do |config|
    if Vagrant.has_plugin?("vagrant-env")
        config.env.load('.env', '.env.local')
    end
    config.vm.box = "bento/ubuntu-20.04"
    config.vm.network "forwarded_port", guest: 1080, host: default_i('VPN_SOCKS_PORT', 1080)
    config.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbook.yml"
      ansible.extra_vars = {
        # there will be error during provisiong when new vpn connection will be added when VPN_GATEWAY is empty
        vpn_gateway: default_s('VPN_GATEWAY', '')
        vpn_ipsec_psk: default_s('VPN_IPSEC_PSK', '')
        vpn_user: default_s('VPN_USER', '')
        vpn_password: default_s('VPN_PASSWORD', '')
      }
    end
  end

  def default_s(key, default)
    ENV[key] && ENV[key].empty? ? ENV[key] : default
  end

  def default_i(key, default)
    default_s(key, default).to_i
  end
  