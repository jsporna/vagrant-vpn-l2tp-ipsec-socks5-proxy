# vagrant-vpn-l2tp-ipsec-socks5-proxy

The Vagrant project will provision VM with configured VPN L2TP+IPsec connection and SOCKS5 proxy for this connection

## Quick start

1. Clone this repository `git clone https://github.com/jsporna/vagrant-vpn-l2tp-ipsec-socks5-proxy.git`
2. Change into the `vagrant-vpn-l2tp-ipsec-socks5-proxy` directory
3. Run `vagrant up; vagrant ssh -c 'vpn-up'`

VPN Connection is up and SOCKS proxy listen on `localhost:1080`

## Configuration

The Vagrant projecxt can be uses _as-is_; there are a couple of parameters you have to set up installation.

### How to configure

There are several ways to set parameters:

1. Update the Vagrantfile. This is straightforward; the downside is that you will loose changes when you update this repository.
2. Use environment variables. Might be difficult to remember the parameters used when the VM was instantiated.
3. Use the `.env` / `.env.local` files (requires [vagrant-env](https://github.com/gosuri/vagrant-env) plugin). Configure your VPN connection by editing the `.env` file; or better copy `.env` to `.env.local` and edit the latter one, it won't be overridden when you update this repository and it won't mark your git tree as changed (you won't accidentally commit your local configuration!)

Parameters are considered in the following order (first one wins):

1. Environment variables
2. `.env.local` (if [vagrant-env](https://github.com/gosuri/vagrant-env) plugin is installed)
3. `.env` (if [vagrant-env](https://github.com/gosuri/vagrant-env) plugin is installed)
4. Vagrantfile definitions

### VPN connection parameters

- `VPN_GATEWAY`: VPN gateway
- `VPN_IPSEC_PSK`: VPN shared secret
- `VPN_USER`: VPN username
- `VPN_PASSWORD`: VPN user password

## Optional plugins

When installed, this Vagrant project will make use of the following third party Vagrant plugins:

- [vagrant-env](https://github.com/gosuri/vagrant-env): loads environment variables from .env files
- [vagrant-exec](https://github.com/p0deje/vagrant-exec): allow in userfriendly way run scripts in Vagrant VM

To install Vagrant plugins run:

```shell
vagrant plugin install <name>...
```

## Feedback

Please provide feedback of any kind via Github issues on this repository.