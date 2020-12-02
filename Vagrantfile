Vagrant.configure("2") do |config|
    if Vagrant.has_plugin?("vagrant-env")
        config.env.load('.env.local', '.env')
    end

    # required
    VPN_GATEWAY = default_s('VPN_GATEWAY', '')
    VPN_IPSEC_PSK = default_s('VPN_IPSEC_PSK', '')
    VPN_USER = default_s('VPN_USER', '')
    VPN_PASSWORD = default_s('VPN_PASSWORD', '')

    # optional
    VPN_SOCKS_PORT = default_i('VPN_SOCKS_PORT', 1080)
end

def default_s(key, default)
ENV[key] && ! ENV[key].empty? ? ENV[key] : default
end

def default_i(key, default)
default_s(key, default).to_i
end
  
Vagrant.configure("2") do |config|
    config.vm.box = "bento/ubuntu-20.04"
    config.vm.network "forwarded_port", guest: 1080, host: VPN_SOCKS_PORT

    config.vm.provision "ansible" do |ansible|
        ansible.playbook = "playbook.yml"
        ansible.extra_vars = {
            vpn_gateway: VPN_GATEWAY,
            vpn_ipsec_psk: VPN_IPSEC_PSK,
            vpn_user: VPN_USER,
            vpn_password: VPN_PASSWORD
        }
    end
end
