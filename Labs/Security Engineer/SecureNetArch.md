# VyOS Zone-Based Firewall Configuration

This repository contains a production-ready, zone-based stateful firewall configuration for VyOS. It implements standard security zones (**WAN**, **LAN**, and **LOCAL**) along with global state tracking to minimize code duplication.

## Configuration Commands

```text
# -----------------------------------------------------------------
# 1. Define Firewall Groups & Global Stateful Tracking
# -----------------------------------------------------------------
set firewall global-options state-policy established action 'accept'
set firewall global-options state-policy related action 'accept'
set firewall global-options state-policy invalid action 'drop'

# Define network groups for easy management
set firewall group network-group LAN_NET network '192.168.10.0/24'

# -----------------------------------------------------------------
# 2. Define Firewall Rule Sets (Filter Rules)
# -----------------------------------------------------------------

# --- LAN to WAN (Allow Outbound Internet) ---
set firewall name LAN-to-WAN default-action 'drop'
set firewall name LAN-to-WAN rule 10 action 'accept'
set firewall name LAN-to-WAN rule 10 description 'Allow LAN to access Internet'
set firewall name LAN-to-WAN rule 10 source group network-group 'LAN_NET'

# --- WAN to LOCAL (Protecting the Router from Internet) ---
set firewall name WAN-to-LOCAL default-action 'drop'
set firewall name WAN-to-LOCAL rule 10 action 'accept'
set firewall name WAN-to-LOCAL rule 10 description 'Allow WireGuard VPN inbound'
set firewall name WAN-to-LOCAL rule 10 destination port '51820'
set firewall name WAN-to-LOCAL rule 10 protocol 'udp'

# --- LAN to LOCAL (Managing the Router from Internal Network) ---
set firewall name LAN-to-LOCAL default-action 'drop'
set firewall name LAN-to-LOCAL rule 10 action 'accept'
set firewall name LAN-to-LOCAL rule 10 description 'Allow Internal SSH'
set firewall name LAN-to-LOCAL rule 10 destination port '22'
set firewall name LAN-to-LOCAL rule 10 protocol 'tcp'
set firewall name LAN-to-LOCAL rule 10 source group network-group 'LAN_NET'

set firewall name LAN-to-LOCAL rule 20 action 'accept'
set firewall name LAN-to-LOCAL rule 20 description 'Allow Internal DNS requests'
set firewall name LAN-to-LOCAL rule 20 destination port '53'
set firewall name LAN-to-LOCAL rule 20 protocol 'tcp,udp'

# -----------------------------------------------------------------
# 3. Create Zone-Based Policy Structure
# -----------------------------------------------------------------
set firewall zone LAN default-action 'drop'
set firewall zone LAN interface 'eth1'
set firewall zone LAN from WAN action 'drop'

set firewall zone WAN default-action 'drop'
set firewall zone WAN interface 'eth0'
set firewall zone WAN from LAN action 'name'
set firewall zone WAN from LAN name 'LAN-to-WAN'

set firewall zone LOCAL default-action 'drop'
set firewall zone LOCAL local-zone
set firewall zone LOCAL from WAN action 'name'
set firewall zone LOCAL from WAN name 'WAN-to-LOCAL'
set firewall zone LOCAL from LAN action 'name'
set firewall zone LOCAL from LAN name 'LAN-to-LOCAL'
