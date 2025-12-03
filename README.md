# Ansible Role nftables
[![CI](https://github.com/supertarto/ansible-role-nftables/actions/workflows/ci.yml/badge.svg)](https://github.com/supertarto/ansible-role-nftables/actions/workflows/ci.yml)


Install and configure nftables for Debian with Ansible.

## Tested plateform
* Debian 12 (Bookworm)
* Debian 13 (Trixie)

## Role variables
Log related variables: Rate limite and burst, to prevent DDoS. Log level.
```yml
nftables_log_rate_limit: "20/second"
nftables_log_burst: "50"
nftables_log_level: "info"
```

Allow SMTP from localhost.
```yml
nftables_allow_loopback_smtp: true
```

List of allowed port, without source or destination restriction. TCP and UDP are separated, Input and Output too.
```yml
nftables_input_allowed_tcp_port: []
# Exemple:
# - "80"
# - "443"

nftables_allowed_output_tcp_ports: []
# Exemple:
# - "80"
# - "443"

nftables_input_allowed_udp_port: []
# Exemple:
# - "53"
# - "123"

nftables_allowed_output_udp_ports: []
# Exemple:
# - "53"
# - "123"
```

List of Allowed source IP and specific port, for more restricted access. TCP and UDP in separated variables.
```yml
nftables_allowed_restricted_input_tcp_ports: []
# Exemple:
#   - ip: "192.168.1.100"
#     port: 3306
#   - ip: "10.0.0.0/8"
#     port: 5432

nftables_allowed_restricted_input_udp_ports: []
# Exemple:
#   - ip: "192.168.1.100"
#     port: 161
```

Allowed TCP transfer (IP source + sport + dport)
```yml
nftables_input_transfert_allowed_tcp_port: []
# Exemple:
#   - ip: "10.0.0.50"
#     sport: 12345
#     dport: 8080
```

List of blacklisted IP. Everything coming from those adresses will be dropped.
```yml
# Drop specific adresses
nftables_drop_specific_adress: []
# Exemple:
#   - "1.2.3.4"
#   - "5.6.7.0/24"
```

Il you have some custom rules that don't fit in case above.
```yml
nftables_custom_input_rules: []
# Exemple:
#   - "ip saddr 10.0.0.0/8 tcp dport 9000 accept comment \"Custom service\""
#   - "udp dport 1300 accept comment \"Other Service\"

nftables_custom_output_rules: []
nftables_custom_forward_rules: []
```

## License
GPL V3.0
